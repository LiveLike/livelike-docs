---
title: List Collection Items
excerpt: >-
  Returns a paginated list of items (Cards, Dashboards, and Documents) inside
  the specified Collection. Use the `models` query parameter to restrict results
  to a specific type. Use `limit` and `offset` to paginate through large
  Collections.


  **Extracting IDs for downstream calls:**

  - For `model: "card"` items → use `id` as `card_id` in `GET /api/card/{id}`
  and the Card download endpoint.

  - For `model: "dashboard"` items → use `id` as `dashboard_id` in `GET
  /api/dashboard/{id}` and the Dashboard download endpoint.


  > **Note:** `total` may be `null` when the Collection is empty. Always check
  `data.length` rather than relying on `total`.
api:
  file: analytics_schema.json
  operationId: get_collection_items
hidden: false
---