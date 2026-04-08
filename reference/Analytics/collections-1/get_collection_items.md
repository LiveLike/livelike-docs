---
title: List Collection Items
excerpt: >-
  Lists Cards, Dashboards, and Documents inside a Collection.


  - Cards (`model: "card"`) → use `id` as `card_id` to download data.

  - Dashboards (`model: "dashboard"`) → use `id` to get `dashcard_id` and
  `card_id`.


  > `total` can be null on empty Collections. Use `data.length` instead.
api:
  file: livelike-analytics-api.json
  operationId: get_collection_items
hidden: false
---