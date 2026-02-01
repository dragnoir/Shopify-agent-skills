# GraphQL Query Examples

Common GraphQL queries and mutations for Shopify development.

## Product Queries

### Get Products with Full Details

```graphql
query GetProducts($first: Int!, $query: String, $after: String) {
  products(first: $first, query: $query, after: $after) {
    pageInfo {
      hasNextPage
      hasPreviousPage
      startCursor
      endCursor
    }
    nodes {
      id
      title
      handle
      description
      descriptionHtml
      status
      vendor
      productType
      tags
      createdAt
      updatedAt
      publishedAt

      options {
        id
        name
        position
        values
      }

      featuredImage {
        id
        url
        altText
        width
        height
      }

      images(first: 10) {
        nodes {
          id
          url
          altText
        }
      }

      variants(first: 100) {
        nodes {
          id
          title
          sku
          barcode
          price
          compareAtPrice
          inventoryQuantity
          weight
          weightUnit
          selectedOptions {
            name
            value
          }
          image {
            url
          }
        }
      }

      priceRangeV2 {
        minVariantPrice {
          amount
          currencyCode
        }
        maxVariantPrice {
          amount
          currencyCode
        }
      }

      seo {
        title
        description
      }

      metafields(first: 10) {
        nodes {
          namespace
          key
          value
          type
        }
      }
    }
  }
}
```

### Get Single Product

```graphql
query GetProduct($id: ID!) {
  product(id: $id) {
    id
    title
    handle
    variants(first: 100) {
      nodes {
        id
        title
        price
        inventoryQuantity
      }
    }
  }
}
```

## Order Queries

### Get Orders with Details

```graphql
query GetOrders($first: Int!, $query: String) {
  orders(first: $first, query: $query, sortKey: CREATED_AT, reverse: true) {
    nodes {
      id
      name
      email
      phone
      createdAt
      processedAt
      closedAt
      cancelledAt

      displayFinancialStatus
      displayFulfillmentStatus

      totalPriceSet {
        shopMoney {
          amount
          currencyCode
        }
      }

      subtotalPriceSet {
        shopMoney {
          amount
          currencyCode
        }
      }

      totalShippingPriceSet {
        shopMoney {
          amount
          currencyCode
        }
      }

      totalTaxSet {
        shopMoney {
          amount
          currencyCode
        }
      }

      totalDiscountsSet {
        shopMoney {
          amount
          currencyCode
        }
      }

      customer {
        id
        firstName
        lastName
        email
        phone
      }

      billingAddress {
        firstName
        lastName
        company
        address1
        address2
        city
        province
        provinceCode
        country
        countryCode
        zip
        phone
      }

      shippingAddress {
        firstName
        lastName
        company
        address1
        address2
        city
        province
        provinceCode
        country
        countryCode
        zip
        phone
      }

      lineItems(first: 50) {
        nodes {
          id
          title
          quantity
          sku
          originalTotalSet {
            shopMoney {
              amount
              currencyCode
            }
          }
          variant {
            id
            title
            sku
            product {
              id
              title
            }
          }
        }
      }

      fulfillments {
        id
        status
        trackingInfo {
          company
          number
          url
        }
      }
    }
  }
}
```

## Customer Queries

### Get Customers

```graphql
query GetCustomers($first: Int!, $query: String) {
  customers(first: $first, query: $query) {
    nodes {
      id
      firstName
      lastName
      email
      phone
      verifiedEmail
      taxExempt

      ordersCount
      totalSpent

      addresses(first: 5) {
        address1
        address2
        city
        province
        country
        zip
        phone
      }

      defaultAddress {
        address1
        city
        country
      }

      tags
      note

      createdAt
      updatedAt
    }
  }
}
```

## Inventory Queries

### Get Inventory Levels

```graphql
query GetInventory($locationId: ID!, $first: Int!) {
  location(id: $locationId) {
    id
    name
    inventoryLevels(first: $first) {
      nodes {
        id
        available
        incoming
        item {
          id
          sku
          variant {
            id
            displayName
            product {
              id
              title
            }
          }
        }
      }
    }
  }
}
```

## Mutations

### Create Product

```graphql
mutation CreateProduct($input: ProductInput!) {
  productCreate(input: $input) {
    product {
      id
      title
      handle
      variants(first: 10) {
        nodes {
          id
          price
        }
      }
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "input": {
    "title": "New Product",
    "productType": "Accessories",
    "vendor": "My Brand",
    "descriptionHtml": "<p>Product description</p>",
    "tags": ["new", "featured"],
    "variants": [
      {
        "price": "29.99",
        "sku": "SKU-001",
        "inventoryManagement": "SHOPIFY",
        "inventoryPolicy": "DENY",
        "inventoryQuantities": {
          "availableQuantity": 100,
          "locationId": "gid://shopify/Location/123"
        }
      }
    ]
  }
}
```

### Update Product

```graphql
mutation UpdateProduct($input: ProductInput!) {
  productUpdate(input: $input) {
    product {
      id
      title
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "input": {
    "id": "gid://shopify/Product/123456",
    "title": "Updated Title",
    "status": "ACTIVE"
  }
}
```

### Set Metafields

```graphql
mutation SetMetafields($metafields: [MetafieldsSetInput!]!) {
  metafieldsSet(metafields: $metafields) {
    metafields {
      id
      namespace
      key
      value
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "metafields": [
    {
      "ownerId": "gid://shopify/Product/123456",
      "namespace": "custom",
      "key": "care_instructions",
      "value": "Machine wash cold",
      "type": "single_line_text_field"
    }
  ]
}
```

### Adjust Inventory

```graphql
mutation AdjustInventory($input: InventoryAdjustQuantitiesInput!) {
  inventoryAdjustQuantities(input: $input) {
    inventoryAdjustmentGroup {
      reason
      changes {
        name
        delta
      }
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "input": {
    "name": "Stock correction",
    "reason": "correction",
    "changes": [
      {
        "inventoryItemId": "gid://shopify/InventoryItem/123",
        "locationId": "gid://shopify/Location/456",
        "delta": 10
      }
    ]
  }
}
```

### Create Customer

```graphql
mutation CreateCustomer($input: CustomerInput!) {
  customerCreate(input: $input) {
    customer {
      id
      email
      firstName
      lastName
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "input": {
    "email": "customer@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "phone": "+1234567890",
    "addresses": [
      {
        "address1": "123 Main St",
        "city": "New York",
        "province": "NY",
        "country": "US",
        "zip": "10001"
      }
    ],
    "tags": ["vip", "newsletter"]
  }
}
```

## Webhook Subscriptions

### Create Webhook

```graphql
mutation CreateWebhook($topic: WebhookSubscriptionTopic!, $webhookSubscription: WebhookSubscriptionInput!) {
  webhookSubscriptionCreate(topic: $topic, webhookSubscription: $webhookSubscription) {
    webhookSubscription {
      id
      topic
      endpoint {
        ... on WebhookHttpEndpoint {
          callbackUrl
        }
      }
    }
    userErrors {
      field
      message
    }
  }
}

# Variables
{
  "topic": "ORDERS_CREATE",
  "webhookSubscription": {
    "callbackUrl": "https://your-app.com/webhooks/orders",
    "format": "JSON"
  }
}
```

### List Webhooks

```graphql
query ListWebhooks {
  webhookSubscriptions(first: 50) {
    nodes {
      id
      topic
      endpoint {
        ... on WebhookHttpEndpoint {
          callbackUrl
        }
      }
      createdAt
    }
  }
}
```
