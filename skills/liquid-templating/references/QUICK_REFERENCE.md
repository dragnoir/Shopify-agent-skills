# Liquid Quick Reference

A quick reference for commonly used Liquid patterns in Shopify themes.

## Objects Quick Reference

### Global Objects

```liquid
{{ shop.name }}
{{ shop.email }}
{{ shop.url }}
{{ request.locale.iso_code }}
{{ request.page_type }}
{{ settings.primary_color }}
```

### Page-Specific Objects

```liquid
{{ product }}          <!-- Product pages -->
{{ collection }}       <!-- Collection pages -->
{{ article }}          <!-- Blog articles -->
{{ blog }}             <!-- Blog pages -->
{{ page }}             <!-- Static pages -->
{{ cart }}             <!-- Cart page -->
{{ customer }}         <!-- Logged in customer -->
```

## Filter Quick Reference

### String Filters

| Filter          | Example                                        | Output         |
| --------------- | ---------------------------------------------- | -------------- |
| `upcase`        | `{{ 'hello' \| upcase }}`                      | HELLO          |
| `downcase`      | `{{ 'HELLO' \| downcase }}`                    | hello          |
| `capitalize`    | `{{ 'hello' \| capitalize }}`                  | Hello          |
| `strip`         | `{{ '  hi  ' \| strip }}`                      | hi             |
| `truncate`      | `{{ 'hello world' \| truncate: 5 }}`           | he...          |
| `truncatewords` | `{{ 'hello world test' \| truncatewords: 2 }}` | hello world... |
| `replace`       | `{{ 'hello' \| replace: 'l', 'L' }}`           | heLLo          |
| `append`        | `{{ 'hello' \| append: ' world' }}`            | hello world    |
| `prepend`       | `{{ 'world' \| prepend: 'hello ' }}`           | hello world    |
| `split`         | `{{ 'a,b,c' \| split: ',' }}`                  | ['a','b','c']  |
| `size`          | `{{ 'hello' \| size }}`                        | 5              |

### Number Filters

| Filter       | Example                     | Output |
| ------------ | --------------------------- | ------ |
| `plus`       | `{{ 5 \| plus: 3 }}`        | 8      |
| `minus`      | `{{ 5 \| minus: 3 }}`       | 2      |
| `times`      | `{{ 5 \| times: 3 }}`       | 15     |
| `divided_by` | `{{ 10 \| divided_by: 3 }}` | 3      |
| `modulo`     | `{{ 10 \| modulo: 3 }}`     | 1      |
| `round`      | `{{ 4.67 \| round }}`       | 5      |
| `ceil`       | `{{ 4.1 \| ceil }}`         | 5      |
| `floor`      | `{{ 4.9 \| floor }}`        | 4      |

### Array Filters

| Filter    | Example                                | Output        |
| --------- | -------------------------------------- | ------------- |
| `first`   | `{{ array \| first }}`                 | First item    |
| `last`    | `{{ array \| last }}`                  | Last item     |
| `join`    | `{{ array \| join: ', ' }}`            | Joined string |
| `size`    | `{{ array \| size }}`                  | Count         |
| `sort`    | `{{ array \| sort }}`                  | Sorted array  |
| `reverse` | `{{ array \| reverse }}`               | Reversed      |
| `uniq`    | `{{ array \| uniq }}`                  | Unique values |
| `compact` | `{{ array \| compact }}`               | Remove nil    |
| `map`     | `{{ products \| map: 'title' }}`       | Titles array  |
| `where`   | `{{ products \| where: 'available' }}` | Filtered      |

### Money Filters

| Filter                         | Example                                      | Output     |
| ------------------------------ | -------------------------------------------- | ---------- |
| `money`                        | `{{ 1999 \| money }}`                        | $19.99     |
| `money_with_currency`          | `{{ 1999 \| money_with_currency }}`          | $19.99 USD |
| `money_without_currency`       | `{{ 1999 \| money_without_currency }}`       | 19.99      |
| `money_without_trailing_zeros` | `{{ 2000 \| money_without_trailing_zeros }}` | $20        |

### URL Filters

| Filter        | Usage                                     |
| ------------- | ----------------------------------------- |
| `asset_url`   | `{{ 'style.css' \| asset_url }}`          |
| `image_url`   | `{{ image \| image_url: width: 500 }}`    |
| `file_url`    | `{{ 'file.pdf' \| file_url }}`            |
| `product_url` | `{{ product.url }}`                       |
| `within`      | `{{ product.url \| within: collection }}` |

## Common Patterns

### Product Card

```liquid
{% for product in collection.products %}
  <div class="product-card">
    {{ product.featured_image | image_url: width: 400 | image_tag }}
    <h3>{{ product.title }}</h3>
    <p>{{ product.price | money }}</p>
    <a href="{{ product.url }}">View</a>
  </div>
{% endfor %}
```

### Sale Badge

```liquid
{% if product.compare_at_price > product.price %}
  {% assign savings = product.compare_at_price | minus: product.price %}
  {% assign percent = savings | times: 100.0 | divided_by: product.compare_at_price | round %}
  <span class="sale-badge">{{ percent }}% OFF</span>
{% endif %}
```

### Responsive Images

```liquid
{{ image | image_url: width: 1200 | image_tag:
  loading: 'lazy',
  widths: '300, 600, 900, 1200',
  sizes: '(max-width: 600px) 100vw, 50vw'
}}
```

### Pagination

```liquid
{% paginate collection.products by 12 %}
  {% for product in collection.products %}
    {% render 'product-card', product: product %}
  {% endfor %}

  {{ paginate | default_pagination }}
{% endpaginate %}
```

### Cart Form

```liquid
{% form 'product', product %}
  <select name="id">
    {% for variant in product.variants %}
      <option value="{{ variant.id }}">{{ variant.title }}</option>
    {% endfor %}
  </select>
  <input type="number" name="quantity" value="1" min="1">
  <button type="submit">Add to Cart</button>
{% endform %}
```

### Conditional Classes

```liquid
{% assign classes = 'product' %}
{% if product.available == false %}
  {% assign classes = classes | append: ' sold-out' %}
{% endif %}
{% if product.compare_at_price > product.price %}
  {% assign classes = classes | append: ' on-sale' %}
{% endif %}
<div class="{{ classes }}">
```

### Translation with Fallback

```liquid
{% assign button_text = 'products.add_to_cart' | t %}
{% if button_text == blank %}
  {% assign button_text = 'Add to Cart' %}
{% endif %}
```

### Metafield Access

```liquid
{{ product.metafields.custom.care_instructions }}
{{ product.metafields.custom.dimensions.value | json }}
```

## Control Flow

### If/Elsif/Else

```liquid
{% if product.available %}
  In Stock
{% elsif product.selected_or_first_available_variant %}
  Low Stock
{% else %}
  Sold Out
{% endif %}
```

### Unless

```liquid
{% unless product.available %}
  Sold Out
{% endunless %}
```

### Case/When

```liquid
{% case product.type %}
  {% when 'Shirt' %}
    Shirt content
  {% when 'Pants' %}
    Pants content
  {% else %}
    Default content
{% endcase %}
```

### For Loop with Variables

```liquid
{% for product in collection.products limit: 4 %}
  {{ forloop.index }}      <!-- 1, 2, 3, 4 -->
  {{ forloop.index0 }}     <!-- 0, 1, 2, 3 -->
  {{ forloop.first }}      <!-- true/false -->
  {{ forloop.last }}       <!-- true/false -->
  {{ forloop.length }}     <!-- total count -->
{% else %}
  No products found
{% endfor %}
```

## Comparison Operators

| Operator   | Meaning               |
| ---------- | --------------------- |
| `==`       | Equal                 |
| `!=`       | Not equal             |
| `>`        | Greater than          |
| `<`        | Less than             |
| `>=`       | Greater or equal      |
| `<=`       | Less or equal         |
| `contains` | Contains string/array |
| `and`      | Logical AND           |
| `or`       | Logical OR            |

## Resources

- [Liquid Reference](https://shopify.dev/docs/api/liquid)
- [Liquid Cheat Sheet](https://www.shopify.com/partners/shopify-cheat-sheet)
