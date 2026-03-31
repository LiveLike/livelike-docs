---
title: List Collections
excerpt: >-
  Returns a flat array of all Collections accessible to your API key. Use the
  returned `id` values to list the contents of a Collection via `GET
  /api/collection/{id}/items`.


  **When to use vs. `/api/collection/tree`:** Use this endpoint when you need a
  flat list without hierarchy. Use `/api/collection/tree` when you need the
  nested parent-child structure in a single call.


  > **Note:** The root Collection has `id: "root"` (a string). All other
  Collection IDs are integers.
api:
  file: analytics_schema.json
  operationId: get_collections
hidden: false
---