---
title: List Collection Items
excerpt: >-
  Lists the Cards, Dashboards, and Documents inside a Collection. Use `models`
  to filter by type, and `limit`/`offset` to page through large Collections.


  - Cards (`model: "card"`) → use `id` as `card_id` in `GET /api/card/{id}` and
  the Card download endpoint.

  - Dashboards (`model: "dashboard"`) → use `id` as `dashboard_id` in `GET
  /api/dashboard/{id}` and the Dashboard download endpoint.


  > **Note:** `total` can be null when the Collection is empty. Check
  `data.length` instead.
api:
  file: livelike-analytics-api.json
  operationId: get_collection_items
hidden: false
---