# Shopify Theme Khors - Documentation

Documentation site for Khors Shopify theme, built with **Astro 6** + **Tailwind CSS v4** + **shadcn/ui v4** + **Cloudflare Workers**.

**Live:** [khors.design4.pro](https://khors.design4.pro)

## Tech Stack

| Component | Technology |
|-----------|-------------|
| Framework | Astro 6.x |
| Styling | Tailwind CSS v4 |
| UI Components | shadcn/ui v4 (Base UI) |
| Deployment | Cloudflare Workers |
| Domain | khors.design4.pro |

## Quick Start

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

## Deployment

### CI/CD (GitHub Actions)

Push to `main` branch triggers automatic deployment to Cloudflare Workers.

Required Secrets in GitHub:
- `CLOUDFLARE_API_TOKEN` - Cloudflare API token
- `CLOUDFLARE_ACCOUNT_ID` - Cloudflare account ID

### Manual Deploy

```bash
pnpm build
wrangler deploy
```

## Adding Components

```bash
# Add a component
npx shadcn@latest add button

# Add multiple components
npx shadcn@latest add card badge
```

## Project Structure

```
src/
├── components/
│   └── ui/           # shadcn/ui components
├── layouts/          # Astro layouts
├── lib/              # Utilities
├── pages/            # Astro pages
└── styles/
    └── global.css    # Tailwind + shadcn styles
```

## Scripts

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start development server |
| `pnpm build` | Build for production |
| `pnpm preview` | Preview production build |
| `pnpm generate-types` | Generate Wrangler types |
