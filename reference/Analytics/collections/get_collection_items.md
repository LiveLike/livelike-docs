---
title: List Collection Items
excerpt: >-
  Lists the Cards, Dashboards, and Documents inside a Collection. Use `models`
  to filter by type. Use `limit` and `offset` to page through large Collections.


  **Grabbing IDs for next steps:**

  - `model: "card"` items → use `id` as `card_id` in `GET /api/card/{id}` and
  the Card download endpoint.

  - `model: "dashboard"` items → use `id` as `dashboard_id` in `GET
  /api/dashboard/{id}` and the Dashboard download endpoint.


  > **Note:** `total` can be null when the Collection is empty. Check
  `data.length` instead of relying on `total`.
api:
  file: analytics_schema.json
  operationId: get_collection_items
hidden: false
---