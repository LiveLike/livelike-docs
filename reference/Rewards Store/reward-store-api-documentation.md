---
title: Reward Store API documentation
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The  Rewards Store API is a comprehensive reward management system. It provides endpoints for managing reward products, processing redemptions, tracking orders, and managing user rewards.

**Base URL**: [https://example.com](https://example.com)
**Authentication**: Bearer Token (Store API Access Token)

<br />

### Authentication

Most endpoints require authentication using a Bearer token in the Authorization header:
Authorization: Bearer STORE_API_ACCESS_TOKEN
Required for:

* Order management endpoints
* Redeem endpoint
* User-specific operations

Not required for:

* Public product listings
* Category listings
* Badge listings
* Reward item listings

<br />

### Error Handling

The API uses standard HTTP status codes and returns detailed error information:

```Text Error Handling
{
  "error": {
    "status": 400,
    "name": "BadRequestError",
    "message": "Detailed error message",
    "details": {
      "errorCode": "40001",
      "additionalInfo": "Additional context"
    }
  }
}

```

<br />

### Rate Limiting

The API implements rate limiting to ensure fair usage.

Rate limit headers are included in responses:

* X-RateLimit-Limit: Maximum requests per time window
* X-RateLimit-Remaining: Remaining requests in current window
* X-RateLimit-Reset: Time when the rate limit resets

<br />

## Endpoints

### Products

##### GET /api/products

Retrieve all available reward products with optional filtering and pagination.
Parameters:

* populate (string): Populate relations (* for all, specific relations like reward,categories)
* filters[categories][id][$eq] (number): Filter by category ID
* sort (string): Sort order (e.g., createdAt:desc, name:asc)
* pagination[page] (number): Page number (default: 1)
* pagination[pageSize] (number): Items per page (default: 25, max: 100)
* publicationState (string): live or preview (default: live)

<br />

**Example Request:**

```Text Request
GET /api/products?populate=*&filters[categories][id][$eq]=1&sort=createdAt:desc
```

**Example Response:**

```Text Response
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Premium Reward Item",
        "description": [
          {
            "type": "paragraph",
            "children": [
              {
                "type": "text",
                "text": "Exclusive premium reward item"
              }
            ]
          }
        ],
        "maxRedemptionCount": 1,
        "inventoryCount": 50,
        "inventoryProvider": "METS",
        "startAt": "2024-01-01T00:00:00.000Z",
        "expiryAt": "2024-12-31T23:59:59.000Z",
        "hasProductVariants": false,
        "createdAt": "2024-01-15T10:00:00.000Z",
        "updatedAt": "2024-01-15T10:00:00.000Z",
        "publishedAt": "2024-01-15T10:00:00.000Z",
        "productImage": {
          "data": {
            "id": 1,
            "attributes": {
              "url": "/uploads/product_image.jpg",
              "alternativeText": "Product Image"
            }
          }
        },
        "categories": {
          "data": [
            {
              "id": 1,
              "attributes": {
                "name": "Electronics",
                "categorySequence": 1
              }
            }
          ]
        },
        "reward": {
          "id": 1,
          "rewardItemCost": 100,
          "hasDiscountedCost": false,
          "rewardItemDiscountedCost": null,
          "rewardItem": {
            "data": {
              "id": 1,
              "attributes": {
                "name": "Points",
                "livelikeRewardItemId": "reward-item-123"
              }
            }
          }
        }
      }
    }
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "pageSize": 25,
      "pageCount": 1,
      "total": 1
    }
  }
}
```

<br />

#### GET /api/products/:id

Get detailed information about a specific product.

**Parameters**:

* id (number, required): Product ID
* populate (string): Populate relations

**Example Request:**
`GET /api/products/1?populate=*`

<br />

### Categories

#### GET /api/categories

Retrieve all product categories.

**Parameters:**

* populate (string): Populate relations
* sort (string): Sort order (recommended: categorySequence:asc)
* locale (string): Locale for i18n content (default: en)

**Example Request:**

```Text Request
GET /api/categories?populate=*&sort=categorySequence:asc
```

**Example Response:**

```Text Response
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Electronics",
        "description": "Electronic devices and accessories",
        "categorySequence": 1,
        "categoryType": "TIER_BENEFIT",
        "locale": "en",
        "createdAt": "2024-01-15T10:00:00.000Z",
        "updatedAt": "2024-01-15T10:00:00.000Z",
        "publishedAt": "2024-01-15T10:00:00.000Z"
      }
    }
  ]
}
```

<br />

#### GET /api/categories/:id

Get detailed information about a specific category.

**Parameters**:

* id (number, required): Category ID
* populate (string): Populate relations

<br />

### Orders

**Authentication Required**: Bearer Token Additional Header:

* livelike-user-token (string, required): LiveLike user token

#### GET /api/orders

Get orders for the authenticated user.

Parameters:

* `filters[livelikeUserId][$eq] (string): `Filter by user ID` (automatically applied)`
* `filters[status][$eq] (string):` Filter by status `(FULFILLED, REJECTED, PENDING, REFUNDED)`
* populate (string): Populate relations
* sort (string): Sort order (recommended: createdAt:desc)`

<br />

**Example Request**

```Text Request
GET /api/orders?filters[livelikeUserId][$eq]=user123&populate=*&sort=createdAt:desc

Authorization: Bearer STORE_API_ACCESS_TOKEN

livelike-user-token: LIVELIKE_USER_TOKEN
```

**Example Response**

```Text Response
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "transactionId": "uuid-transaction-id",
        "livelikeUserId": "user123",
        "customId": "user-123",
        "status": "FULFILLED",
        "quantity": 1,
        "totalRewardItemAmount": 100,
        "rewardItemId": "reward-item-123",
        "inventoryProvider": "METS",
        "orderRequestedAt": "2024-01-15T10:30:00.000Z",
        "expiryAt": "2024-12-31T23:59:59.000Z",
        "sku": "VARIANT_SKU_001",
        "product": {
          "data": {
            "id": 1,
            "attributes": {
              "name": "Premium Reward Item"
            }
          }
        }
      }
    }
  ]
}

```

<br />

#### GET /api/orders/:id

Get detailed information about a specific order.

**Parameters:**

* id (number, required): Order ID
* populate (string): Populate relations

<br />

### Redeem

**Authentication Required**: Bearer Token Additional Header:

* livelike-user-token (string, required): LiveLike user token

<br />

#### POST /api/redeem

Redeem a reward product for the authenticated user.

**Request Body**

```
{
  "productId": 1,
  "quantity": 1,
  "sku": "VARIANT_SKU_001"
}
```

**Parameters:**

* productId (number, required): ID of the product to redeem
* quantity (number, optional): Quantity to redeem (default: 1)
* sku (string, optional): Product variant SKU (required for products with variants)

**Validation Checks:**

1. Product exists and is available
2. User has sufficient reward points
3. Product inventory is available
4. User hasn’t exceeded max redemption limit
5. Product hasn’t expired
6. User has required badge (if applicable)
7. Product variant exists (if SKU provided)

<br />

**Example Request:**

```Text Example Request
POST /api/redeem
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "productId": 1,
  "quantity": 1,
  "sku": "VARIANT_SKU_001"
}
```

Response:

```Text Success Response (200)
{
  "order": {
    "id": 123,
    "transactionId": "uuid-transaction-id",
    "status": "FULFILLED",
    "quantity": 1,
    "totalRewardItemAmount": 100,
    "orderRequestedAt": "2024-01-15T10:30:00.000Z",
    "product": {
      "id": 1,
      "name": "Premium Reward Item",
      "inventoryCount": 49
    }
  },
  "userRewardPoints": {
    "currentBalance": 900,
    "rewardItemId": "reward-item-123"
  }
}

```
```Text Error Response (400)
{
  "error": {
    "status": 400,
    "name": "BadRequestError",
    "message": "Insufficient reward points",
    "details": {
      "errorCode": "40003",
      "userRewardBalance": 50,
      "productRewardItemCost": 100
    }
  }
}

```

<br />

### Reward Items

#### GET /api/reward-items

Retrieve all reward items.

**Example Response:**

```
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Points",
        "livelikeRewardItemId": "reward-item-123",
        "createdAt": "2024-01-15T10:00:00.000Z",
        "updatedAt": "2024-01-15T10:00:00.000Z"
      }
    }
  ]
}

```

<br />

#### GET /api/reward-items/:id

Get detailed information about a specific reward item.

<br />

### Badges

#### GET /api/badges

Retrieve all badges.

#### GET /api/badges/:id

Get detailed information about a specific badge.

<br />

### Refunds

#### GET /api/refunds

Retrieve all refund records.
**Parameters:**

* populate (string): Populate relations (recommended: * to include order details)

<br />

#### GET /api/refunds/:id

Get detailed information about a specific refund.

<br />

## Data Models

#### Product

```
interface Product {
  id: number;
  name: string;
  description: Block[];
  maxRedemptionCount: number;
  inventoryCount: number;
  inventoryProvider: string;
  startAt?: string;
  expiryAt?: string;
  hasProductVariants: boolean;
  productImage: MediaFile;
  categories: Category[];
  reward?: Reward;
  rewardItem?: RewardItem;
  badge?: Badge;
  variants?: ProductVariant[];
  sponsor?: Sponsor;
  redemptionSuccessMessage: Block[];
  redemptionFailureMessage?: Block[];
}

```

<br />

#### Order

```
interface Order {
  id: number;
  transactionId: string;
  livelikeUserId: string;
  customId: string;
  status: "FULFILLED" | "REJECTED" | "PENDING" | "REFUNDED";
  quantity: number;
  totalRewardItemAmount: number;
  rewardItemId: string;
  inventoryProvider: string;
  orderRequestedAt: string;
  expiryAt?: string;
  sku?: string;
  reason?: string;
  referenceId: string;
  totalBaseRewardItemAmount?: number;
  product: Product;
  refund?: Refund;
}

```

<br />

#### Category

```
interface Category {
  id: number;
  name: string;
  description?: string;
  categorySequence: number;
  categoryType?: "TIER_BENEFIT";
  locale: string;
  products: Product[];
}
```

<br />

#### RewardItem

```
interface RewardItem {
  id: number;
  name: string;
  livelikeRewardItemId: string;
}

```

<br />

#### Refund

```
interface Refund {
  id: number;
  order: Order;
  livelikeUserId: string;
  rewardItemId: string;
  productName: string;   
  inventoryProvider: string;
  amount: number;
  quantity: number;
  sku?: string;
  reason?: string;
}

```

<br />

## Error Codes

| Code  | Description                        |
| :---- | :--------------------------------- |
| 40001 | Product ID missing in request body |
| 40002 | Invalid product ID                 |
| 40003 | Insufficient reward points         |
| 40004 | Insufficient product inventory     |
| 40005 | Maximum redemption limit reached   |
| 40006 | Product has expired                |
| 40007 | Required badge not earned          |
| 40010 | Failed to get user reward points   |
| 40011 | Product variant SKU missing        |
| 40012 | Product variant not found          |

<br />

## Examples

### Complete Redemption Flow

1. Get Available Products
   ```
   GET /api/products?populate=_&filters[categories][id][$eq]=1
   ```
2. Check Product Details

```
GET /api/products/1?populate=_
```

1. Redeem Product
   ```
   POST /api/redeem
   Authorization: Bearer STORE_API_ACCESS_TOKEN
   livelike-user-token: LIVELIKE_USER_TOKEN
   Content-Type: application/json

   {
     "productId": 1,
     "quantity": 1
   }
   ```
2. Check Order Status
   ```
   GET /api/orders?filters[livelikeUserId][$eq]=user123&populate=*
   Authorization: Bearer STORE_API_ACCESS_TOKEN
   livelike-user-token: LIVELIKE_USER_TOKEN
   ```

<br />

### Filtering and Pagination

Get products by category with pagination:

```
GET /api/products?filters[categories][id][$eq]=1&pagination[page]=1&pagination[pageSize]=10&populate=*
```

Get user’s fulfilled orders:

```
GET /api/orders?filters[livelikeUserId][$eq]=user123&filters[status][$eq]=FULFILLED&populate=*&sort=createdAt:desc
Authorization: Bearer STORE_API_ACCESS_TOKEN
livelike-user-token: LIVELIKE_USER_TOKEN
```

<br />

## Integration Notes

* Authentication: Ensure proper Bearer token is included for protected endpoints
* Error Handling: Always check for error responses and handle them appropriately
* Rate Limiting: Implement proper retry logic with exponential backoff
* Caching: The API implements caching for performance; cache headers should be respected
* Pagination: Use pagination for large datasets to improve performance
* Population: Use the populate parameter strategically to get required relations without over-fetching

<br />

## Support

For API support and questions, please contact the development team or refer to the internal documentation for additional technical details.
