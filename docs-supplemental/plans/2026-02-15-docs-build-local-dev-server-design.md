# Design: Docs Build Local Dev Server

**Date:** 2026-02-15
**Author:** Claude Code
**Status:** Approved for implementation

## Problem

The `/docs-build` workflow and screenshot script currently use `https://khors-theme.design4.pro/` which is password-protected, preventing automated screenshot generation.

**Solution:** Switch to local dev server `http://127.0.0.1:9292` with auto-start capability.

---

## Requirements

1. **Auto-start dev server** if not already running
2. **Timeout:** 60 seconds for server to start
3. **Leave running** after screenshots complete
4. **Zero additional files** - modify only existing `screenshot-batch.js` and `docs-build.md`

---

## Architecture

### High-Level Flow

```
MAIN
└─> ensureDevServer()
    ├─> isServerRunning()? → YES → SKIP
    └─> NO → startDevServer() → waitForServer(60s)
└─> captureScreenshots() (unchanged)
```

### Configuration Changes

**File:** `.claude/scripts/screenshot-batch.js`

```javascript
const CONFIG = {
    baseUrl: 'http://127.0.0.1:9292',  // CHANGED from production URL
    devServer: {  // NEW
        timeout: 60000,
        checkInterval: 1000,
        command: 'shopify theme dev --store khors-theme-design4pro.myshopify.com'
    },
    // ... rest unchanged
};
```

---

## Implementation

### 1. Helper Functions

**Add after require statements (~line 15):**

```javascript
const http = require('http');
const { spawn } = require('child_process');
```

**Add before `captureScreenshots()` (~line 100):**

```javascript
/**
 * Sprawdza czy dev server działa na 127.0.0.1:9292
 */
async function isServerRunning() {
    return new Promise((resolve) => {
        const options = {
            hostname: '127.0.0.1',
            port: 9292,
            path: '/',
            method: 'HEAD',
            timeout: 2000
        };

        const req = http.request(options, (res) => {
            resolve(res.statusCode === 200 || res.statusCode === 302);
        });

        req.on('error', () => resolve(false));
        req.on('timeout', () => {
            req.destroy();
            resolve(false);
        });

        req.end();
    });
}

/**
 * Uruchamia Shopify dev server w tle
 */
function startDevServer() {
    console.log('🚀 Starting Shopify dev server...');

    const proc = spawn('shopify', ['theme', 'dev', '--store', 'khors-theme-design4pro.myshopify.com'], {
        detached: true,
        stdio: 'ignore'
    });

    proc.unref(); // Pozwól procesowi działać w tle

    return proc;
}

/**
 * Czeka aż server odpowie (max timeout ms)
 */
async function waitForServer(timeout = 60000) {
    const startTime = Date.now();
    const checkInterval = 1000;

    while (Date.now() - startTime < timeout) {
        if (await isServerRunning()) {
            console.log('✅ Dev server is ready!');
            return true;
        }

        process.stdout.write('.');
        await sleep(checkInterval);
    }

    throw new Error(`Dev server failed to start within ${timeout}ms`);
}

/**
 * Zapewnia że dev server działa
 */
async function ensureDevServer() {
    console.log('🔍 Checking dev server status...');

    if (await isServerRunning()) {
        console.log('✅ Dev server already running');
        return;
    }

    startDevServer();
    await waitForServer(CONFIG.devServer.timeout);
}
```

### 2. Main Flow Integration

**Replace main execution block (~line 254-265):**

```javascript
(async function main() {
    try {
        // 1. Zapewnij że dev server działa
        await ensureDevServer();

        // 2. Wykonaj screenshoty
        const results = await captureScreenshots(sectionName);

        // 3. Opcjonalnie pokaż MDX frames
        if (args.includes('--mdx')) {
            console.log('\nMDX Frames:');
            console.log('===========\n');
            console.log(generateMdxFrames(results));
        }

        process.exit(0);

    } catch (error) {
        console.error('\n❌ Fatal error:', error.message);

        // Szczegółowe komunikaty dla różnych błędów
        if (error.message.includes('Dev server failed to start')) {
            console.error('\nTroubleshooting:');
            console.error('  1. Check if Shopify CLI is installed: shopify version');
            console.error('  2. Check if port 9292 is available: lsof -i :9292');
            console.error('  3. Try starting manually: shopify theme dev --store khors-theme-design4pro.myshopify.com');
        }

        process.exit(1);
    }
})();
```

---

## Workflow Documentation Updates

**File:** `.claude/skills/khors-workflow/docs-build.md`

### Key Changes

1. **New step "Ensure Dev Server Running"** before screenshot generation
2. **Update all URL references** from production to `http://127.0.0.1:9292`
3. **Add troubleshooting section** for dev server issues
4. **Document auto-start behavior** with manual alternative

---

## Error Handling

| Error | Handling |
|-------|----------|
| Dev server timeout | Clear error message + troubleshooting steps |
| Port 9292 occupied | Suggest `lsof -i :9292` and kill command |
| Shopify CLI missing | Suggest `shopify version` check |
| Playwright errors | Already handled in original code |

---

## Testing Plan

1. **Test with server already running:**
   ```bash
   shopify theme dev --store khors-theme-design4pro.myshopify.com
   # In another terminal:
   node .claude/scripts/screenshot-batch.js header
   ```
   Expected: Detects running server, skips auto-start

2. **Test with server not running:**
   ```bash
   # Kill any running server
   kill -9 $(lsof -t -i:9292)
   # Run script
   node .claude/scripts/screenshot-batch.js header
   ```
   Expected: Auto-starts server, waits, then captures

3. **Test timeout scenario:**
   ```bash
   # Block port 9292
   nc -l 9292 &
   # Run script
   node .claude/scripts/screenshot-batch.js header
   ```
   Expected: Timeout error with troubleshooting steps

---

## Rollback Plan

If issues arise, revert by:
1. Change `baseUrl` back to `https://khors-theme.design4pro.myshopify.com`
2. Remove `ensureDevServer()` call from main
3. Remove helper functions
4. Revert workflow documentation

---

## Files Modified

- `.claude/scripts/screenshot-batch.js` - Core implementation
- `.claude/skills/khors-workflow/docs-build.md` - Workflow documentation
- `docs/plans/2026-02-15-docs-build-local-dev-server-design.md` - This design doc

---

## Decision Log

**Why local dev server?**
- Production URL is password-protected
- No way to authenticate Playwright automatically
- Local server is accessible without credentials

**Why auto-start?**
- Better UX - workflow "just works"
- Reduces manual steps
- Follows principle of least surprise

**Why leave server running?**
- User may want to continue using it
- Safer than auto-cleanup (avoid killing user's manual session)
- Follows "do one thing well" principle

**Why 60s timeout?**
- Shopify theme dev typically starts in 10-20s
- 60s provides safe buffer for slower machines
- Long enough to be reliable, short enough to fail fast

---

## Success Criteria

- ✅ Screenshots work without manual dev server start
- ✅ No additional files created
- ✅ Clear error messages when things fail
- ✅ Workflow documentation is accurate
- ✅ Zero breaking changes to existing functionality
