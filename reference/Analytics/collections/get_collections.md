---
title: List Collections
excerpt: >-
  Returns a flat list of all Collections your API key can see. Use the `id`
  values to dig into a specific Collection with `GET
  /api/collection/{id}/items`.


  **Flat list vs. tree:** Use this endpoint when you just need a simple list.
  Use `/api/collection/tree` when you need to see the parent-child nesting in
  one call.


  > **Note:** The root Collection has `id: "root"` (a string). All others have
  integer IDs.
api:
  file: analytics_schema.json
  operationId: get_collections
hidden: false
---