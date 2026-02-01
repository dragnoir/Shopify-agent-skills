# Shopify Theme Directory Structure Reference

This reference provides detailed information about each directory in a Shopify theme.

## Required Files

Only `layout/theme.liquid` is strictly required for a theme to upload to Shopify.

## Directory Breakdown

### `/assets`

Contains all static assets: CSS, JavaScript, images, fonts.

**File Types:**

- CSS files (`.css`)
- JavaScript files (`.js`)
- Images (`.png`, `.jpg`, `.gif`, `.svg`)
- Fonts (`.woff`, `.woff2`)
- Liquid CSS/JS (`.css.liquid`, `.js.liquid`)

**Best Practices:**

- Use descriptive filenames
- Minimize and compress production assets
- Use `image_url` filter for images, not direct asset URLs
- Avoid `.liquid` extension for assets when possible (reduces caching)

**Accessing Assets:**

```liquid
{{ 'style.css' | asset_url | stylesheet_tag }}
{{ 'app.js' | asset_url | script_tag }}
{{ 'logo.png' | asset_url }}
```

---

### `/config`

Contains theme configuration files.

**Files:**

- `settings_schema.json` - Defines theme settings UI
- `settings_data.json` - Stores theme settings values

**settings_schema.json Structure:**

```json
[
  {
    "name": "theme_info",
    "theme_name": "My Theme",
    "theme_version": "1.0.0"
  },
  {
    "name": "Colors",
    "settings": [
      {
        "type": "color",
        "id": "primary_color",
        "label": "Primary color",
        "default": "#000000"
      }
    ]
  }
]
```

**Setting Types:**

- `text`, `textarea`, `richtext`
- `number`, `range`
- `checkbox`
- `radio`, `select`
- `color`, `color_background`
- `font_picker`
- `collection`, `product`, `blog`, `page`, `link_list`, `url`
- `image_picker`, `video`, `video_url`
- `html`, `liquid`

---

### `/layout`

Contains layout files that wrap page content.

**Default Layout:**

```liquid
<!-- layout/theme.liquid -->
<!DOCTYPE html>
<html lang="{{ request.locale.iso_code }}">
<head>
  {{ content_for_header }}
  <title>{{ page_title }}</title>
</head>
<body>
  {% sections 'header-group' %}
  <main>{{ content_for_layout }}</main>
  {% sections 'footer-group' %}
</body>
</html>
```

**Alternative Layouts:**

- `password.liquid` - Password page
- `checkout.liquid` - Checkout (Plus only)
- Custom layouts (used via `layout:` in templates)

---

### `/locales`

Contains translation files for internationalization.

**File Naming:**

- `en.default.json` - Default locale
- `fr.json` - French
- `de.json` - German
- `es.json` - Spanish

**Structure:**

```json
{
  "general": {
    "search": "Search",
    "cart": "Cart",
    "menu": "Menu"
  },
  "products": {
    "add_to_cart": "Add to cart",
    "sold_out": "Sold out"
  }
}
```

**Accessing Translations:**

```liquid
{{ 'general.cart' | t }}
{{ 'products.add_to_cart' | t }}
```

---

### `/sections`

Contains reusable, customizable theme components.

**Section Structure:**

```liquid
{% schema %}
{
  "name": "Section Name",
  "settings": [],
  "blocks": [],
  "presets": []
}
{% endschema %}

{% stylesheet %}
{% endstylesheet %}

{% javascript %}
{% endjavascript %}
```

**Section Groups:**

```json
{
  "type": "header",
  "name": "Header Group",
  "sections": {
    "announcement": { "type": "announcement-bar" },
    "header": { "type": "header" }
  },
  "order": ["announcement", "header"]
}
```

**Accessing Section Settings:**

```liquid
{{ section.settings.heading }}
{{ section.id }}
```

---

### `/snippets`

Contains reusable Liquid code fragments.

**Usage:**

```liquid
{% render 'product-card', product: product %}
{% render 'icon-cart' %}
```

**With Variables:**

```liquid
{% render 'product-card',
  product: product,
  show_price: true,
  lazy_load: true
%}
```

**Common Snippets:**

- `product-card.liquid`
- `collection-card.liquid`
- `icon-*.liquid`
- `price.liquid`
- `social-sharing.liquid`

---

### `/templates`

Contains page templates that define content structure.

**Template Types:**
| Template | Description |
|----------|-------------|
| `index.json` | Home page |
| `product.json` | Product pages |
| `collection.json` | Collection pages |
| `page.json` | Static pages |
| `blog.json` | Blog pages |
| `article.json` | Blog articles |
| `cart.json` | Cart page |
| `search.json` | Search results |
| `404.json` | Not found page |
| `password.json` | Password page |
| `list-collections.json` | Collections list |
| `gift_card.liquid` | Gift card (Liquid only) |

**JSON Template Structure:**

```json
{
  "sections": {
    "main": {
      "type": "main-product",
      "settings": {}
    },
    "recommendations": {
      "type": "product-recommendations",
      "settings": {}
    }
  },
  "order": ["main", "recommendations"]
}
```

**Alternate Templates:**
Create `product.alternate.json` for different layouts:

```json
{
  "name": "Product (No Reviews)",
  "sections": {}
}
```

---

### `/templates/customers`

Contains customer account templates.

**Templates:**

- `account.liquid` - Customer dashboard
- `addresses.liquid` - Address management
- `login.liquid` - Login page
- `register.liquid` - Registration
- `order.liquid` - Order details
- `reset_password.liquid` - Password reset
- `activate_account.liquid` - Account activation

---

## File Size Limits

| File Type   | Max Size |
| ----------- | -------- |
| Single file | 256 KB   |
| Total theme | 50 MB    |
| JSON        | 256 KB   |
| Liquid      | 256 KB   |
| CSS/JS      | 256 KB   |

---

## Resources

- [Theme Architecture](https://shopify.dev/docs/storefronts/themes/architecture)
- [Dawn Theme](https://github.com/Shopify/dawn)
- [Theme Check](https://shopify.dev/docs/themes/tools/theme-check)
