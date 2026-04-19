# Translation Key Contracts

**Branch**: `001-khors-theme` | **Date**: 2026-02-06

## File Structure

| File | Purpose | Access Pattern |
|------|---------|---------------|
| `locales/en.default.json` | Storefront-facing text | `{{ 'key.path' \| t }}` |
| `locales/en.default.schema.json` | Theme editor labels | `"label": "t:key.path"` |

## Naming Convention

Keys follow a dot-separated hierarchy: `{domain}.{component}.{element}`

- Sentence case for all values (e.g., "Add to cart", not "Add To Cart")
- Keys use snake_case (e.g., `add_to_cart`, not `addToCart`)
- Schema keys mirror storefront keys where possible

## en.default.json Structure

```json
{
  "general": {
    "header": "Header",
    "footer": "Footer",
    "search": "Search",
    "cart": "Cart",
    "close": "Close",
    "menu": "Menu",
    "share": "Share",
    "loading": "Loading",
    "no_results": "No results found",
    "view_all": "View all",
    "learn_more": "Learn more"
  },

  "accessibility": {
    "skip_to_content": "Skip to content",
    "close_menu": "Close menu",
    "open_menu": "Open menu",
    "close_cart": "Close cart",
    "open_cart": "Open cart",
    "close_search": "Close search",
    "open_search": "Open search",
    "previous_slide": "Previous slide",
    "next_slide": "Next slide",
    "pause_slideshow": "Pause slideshow",
    "play_slideshow": "Play slideshow",
    "slide_x_of_y": "Slide {{ current }} of {{ total }}",
    "loading": "Loading",
    "star_rating": "{{ rating }} out of {{ max }} stars",
    "zoom_image": "Zoom image",
    "view_in_space": "View in your space",
    "variant_sold_out": "{{ variant }} - Sold out",
    "unit_price_separator": "per"
  },

  "products": {
    "product": {
      "add_to_cart": "Add to cart",
      "sold_out": "Sold out",
      "unavailable": "Unavailable",
      "price": {
        "regular": "Regular price",
        "sale": "Sale price",
        "from": "From {{ price }}",
        "unit_price": "Unit price"
      },
      "quantity": {
        "label": "Quantity",
        "increase": "Increase quantity for {{ title }}",
        "decrease": "Decrease quantity for {{ title }}",
        "input_label": "Quantity for {{ title }}"
      },
      "variant": {
        "select_option": "Select {{ option_name }}",
        "sold_out": "Sold out"
      },
      "media": {
        "view_in_space": "View in your space",
        "view_in_space_label": "View in your space, loads an augmented reality viewer",
        "play_video": "Play video",
        "pause_video": "Pause video"
      },
      "selling_plan": {
        "one_time": "One-time purchase",
        "subscription": "Subscribe & save",
        "frequency": "Delivery every {{ interval }}"
      },
      "local_pickup": {
        "available": "Pick up available at {{ location }}",
        "unavailable": "Pickup not available",
        "check_other_stores": "Check availability at other stores"
      }
    }
  },

  "collections": {
    "sorting": {
      "title": "Sort by",
      "price_ascending": "Price, low to high",
      "price_descending": "Price, high to low",
      "alpha_ascending": "Alphabetically, A-Z",
      "alpha_descending": "Alphabetically, Z-A",
      "date_ascending": "Date, old to new",
      "date_descending": "Date, new to old",
      "best_selling": "Best selling"
    },
    "filtering": {
      "title": "Filter",
      "clear_all": "Clear all",
      "apply": "Apply",
      "results_count": "{{ count }} products",
      "no_results": "No products found with these filters"
    },
    "pagination": {
      "previous": "Previous page",
      "next": "Next page",
      "page": "Page {{ number }}",
      "load_more": "Load more products",
      "current_page": "Page {{ current }} of {{ total }}"
    }
  },

  "cart": {
    "title": "Your cart",
    "empty": "Your cart is empty",
    "continue_shopping": "Continue shopping",
    "subtotal": "Subtotal",
    "checkout": "Check out",
    "remove": "Remove {{ title }}",
    "update": "Update",
    "note": "Add a note to your order",
    "discount": "Discount",
    "shipping_note": "Shipping & taxes calculated at checkout",
    "quantity_error": "Only {{ quantity }} available",
    "item_added": "Item added to cart",
    "selling_plan": "{{ plan_name }}"
  },

  "blogs": {
    "article": {
      "read_more": "Read more",
      "by_author": "By {{ author }}",
      "posted_on": "Posted on {{ date }}",
      "comments_count": "{{ count }} comments",
      "share": "Share this article",
      "back_to_blog": "Back to {{ blog_title }}"
    },
    "comments": {
      "title": "Comments",
      "name_label": "Name",
      "email_label": "Email",
      "comment_label": "Comment",
      "submit": "Post comment",
      "success": "Your comment has been submitted and will appear after approval",
      "error": "Please fill in all required fields"
    }
  },

  "search": {
    "title": "Search results",
    "placeholder": "Search our store",
    "submit": "Search",
    "no_results": "No results found for \"{{ query }}\"",
    "results_count": "{{ count }} results for \"{{ query }}\"",
    "suggestions": "Popular searches"
  },

  "contact": {
    "title": "Contact us",
    "name_label": "Name",
    "email_label": "Email",
    "message_label": "Message",
    "submit": "Send message",
    "success": "Thank you for your message. We'll get back to you shortly.",
    "error": "Please fill in all required fields"
  },

  "newsletter": {
    "label": "Email address",
    "submit": "Subscribe",
    "success": "Thank you for subscribing!",
    "error": "Please enter a valid email address"
  },

  "gift_card": {
    "title": "Gift card",
    "balance": "Card balance: {{ balance }}",
    "code_label": "Gift card code",
    "copy": "Copy code",
    "copied": "Copied!",
    "expires": "Expires {{ date }}",
    "print": "Print gift card",
    "shop_link": "Visit {{ shop_name }}"
  },

  "password": {
    "title": "Opening soon",
    "label": "Enter store password",
    "submit": "Enter",
    "login_title": "Password required",
    "powered_by": "Powered by Shopify"
  },

  "social": {
    "share_on_facebook": "Share on Facebook",
    "share_on_twitter": "Share on Twitter",
    "share_on_pinterest": "Pin on Pinterest",
    "share_via_email": "Share via email"
  }
}
```

## en.default.schema.json Structure

```json
{
  "sections": {
    "all": {
      "color_scheme": {
        "label": "Color scheme"
      },
      "heading": {
        "label": "Heading"
      },
      "subheading": {
        "label": "Subheading"
      },
      "description": {
        "label": "Description"
      },
      "button_text": {
        "label": "Button text"
      },
      "button_link": {
        "label": "Button link"
      },
      "image": {
        "label": "Image"
      }
    },

    "header": {
      "name": "Header",
      "settings": {
        "logo": { "label": "Logo" },
        "logo_width": { "label": "Logo width" },
        "menu": { "label": "Menu" },
        "sticky_header": { "label": "Sticky header" },
        "transparent_header": { "label": "Transparent header" },
        "show_search": { "label": "Show search" },
        "show_account": { "label": "Show account icon" }
      }
    },

    "footer": {
      "name": "Footer",
      "blocks": {
        "menu": { "name": "Menu column" },
        "text": { "name": "Text column" }
      },
      "settings": {
        "show_newsletter": { "label": "Show newsletter" },
        "show_social": { "label": "Show social links" },
        "show_payment_icons": { "label": "Show payment icons" }
      }
    },

    "announcement_bar": {
      "name": "Announcement bar",
      "settings": {
        "text": { "label": "Text" },
        "link": { "label": "Link" },
        "link_new_window": { "label": "Open link in new window" }
      }
    },

    "slideshow": {
      "name": "Slideshow",
      "presets": { "name": "Slideshow" },
      "settings": {
        "autoplay": { "label": "Auto-rotate slides" },
        "speed": { "label": "Change slides every" },
        "height": { "label": "Slide height" }
      },
      "blocks": {
        "slide": { "name": "Slide" }
      }
    },

    "featured_products": {
      "name": "Featured products",
      "presets": { "name": "Featured products" },
      "settings": {
        "collection": { "label": "Collection" },
        "products_to_show": { "label": "Maximum products to show" },
        "columns_desktop": { "label": "Number of columns on desktop" },
        "show_vendor": { "label": "Show vendor" },
        "show_price": { "label": "Show price" },
        "show_badge": { "label": "Show sale/sold out badge" }
      }
    },

    "featured_collections": {
      "name": "Featured collections",
      "presets": { "name": "Featured collections" },
      "settings": {
        "collection_list": { "label": "Collections" },
        "collections_to_show": { "label": "Maximum collections to show" }
      }
    },

    "image_with_text": {
      "name": "Image with text",
      "presets": { "name": "Image with text" },
      "settings": {
        "image_position": {
          "label": "Image position",
          "options": {
            "left": "Left",
            "right": "Right"
          }
        }
      }
    },

    "newsletter": {
      "name": "Newsletter",
      "presets": { "name": "Newsletter" }
    },

    "rich_text": {
      "name": "Rich text",
      "presets": { "name": "Rich text" },
      "settings": {
        "content": { "label": "Content" }
      }
    },

    "video": {
      "name": "Video",
      "presets": { "name": "Video" },
      "settings": {
        "video_url": { "label": "Video URL" },
        "video": { "label": "Shopify-hosted video" },
        "cover_image": { "label": "Cover image" },
        "autoplay": { "label": "Autoplay" },
        "loop": { "label": "Loop" }
      }
    },

    "blog_posts": {
      "name": "Blog posts",
      "presets": { "name": "Blog posts" },
      "settings": {
        "blog": { "label": "Blog" },
        "posts_to_show": { "label": "Maximum posts to show" },
        "show_author": { "label": "Show author" },
        "show_date": { "label": "Show date" }
      }
    },

    "collection_list": {
      "name": "Collection list",
      "presets": { "name": "Collection list" }
    },

    "ingredient_spotlight": {
      "name": "Ingredient spotlight",
      "presets": { "name": "Ingredient spotlight" },
      "blocks": {
        "ingredient": { "name": "Ingredient" }
      }
    },

    "tech_specs_comparison": {
      "name": "Tech specs comparison",
      "presets": { "name": "Tech specs comparison" }
    },

    "room_visualizer": {
      "name": "Room visualizer",
      "presets": { "name": "Room visualizer" }
    },

    "before_after_slider": {
      "name": "Before/after slider",
      "presets": { "name": "Before/after slider" },
      "settings": {
        "before_image": { "label": "Before image" },
        "after_image": { "label": "After image" },
        "before_label": { "label": "Before label" },
        "after_label": { "label": "After label" }
      }
    },

    "testimonials": {
      "name": "Testimonials",
      "presets": { "name": "Testimonials" },
      "blocks": {
        "testimonial": { "name": "Testimonial" }
      }
    }
  },

  "blocks": {
    "button": {
      "name": "Button",
      "settings": {
        "text": { "label": "Button text" },
        "url": { "label": "Button link" },
        "variant": {
          "label": "Style",
          "options": {
            "primary": "Primary",
            "secondary": "Secondary",
            "outline": "Outline",
            "ghost": "Ghost"
          }
        },
        "size": {
          "label": "Size",
          "options": {
            "small": "Small",
            "medium": "Medium",
            "large": "Large"
          }
        },
        "full_width": { "label": "Full width" }
      }
    }
  },

  "settings_schema": {
    "typography": {
      "name": "Typography",
      "primary_font": { "label": "Primary font" },
      "secondary_font": { "label": "Secondary font" },
      "base_size": { "label": "Base font size" }
    },
    "layout": {
      "name": "Layout",
      "page_width": { "label": "Page width" },
      "section_margin": { "label": "Section margin" },
      "grid_gap": { "label": "Grid gap" }
    },
    "colors": {
      "name": "Colors",
      "scheme_label": "Color scheme {{ number }}"
    },
    "social_media": {
      "name": "Social media",
      "facebook": { "label": "Facebook" },
      "instagram": { "label": "Instagram" },
      "twitter": { "label": "Twitter" },
      "youtube": { "label": "YouTube" },
      "tiktok": { "label": "TikTok" },
      "pinterest": { "label": "Pinterest" },
      "linkedin": { "label": "LinkedIn" },
      "snapchat": { "label": "Snapchat" }
    }
  }
}
```

## Key Conventions

1. **All user-facing text** must use translation keys — no hardcoded strings in Liquid
2. **Schema labels** reference `en.default.schema.json` via `"label": "t:path.to.key"`
3. **Storefront text** references `en.default.json` via `{{ 'path.to.key' | t }}`
4. **Interpolation** uses `{{ variable }}` syntax within translation values
5. **Sentence case** for all labels and messages
6. **No pluralization rules** — use count-based keys (`comments_count: "{{ count }} comments"`)
