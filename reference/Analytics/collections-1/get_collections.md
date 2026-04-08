---
title: List All Collections
excerpt: >-
  Returns a flat list of all Collections your API key has access to. Use the
  `id` values to list what's inside with `GET /api/collection/{id}/items`.


  Use `/api/collection/tree` instead when you need the full nested hierarchy in
  one call.


  > **Note:** The root Collection has `id: "root"` (a string). All others use
  integer IDs.


  > **Tip:** Filter out items where `is_personal: true` — these are individual
  user folders, not shared analytics content.
api:
  file: livelike-analytics-api.json
  operationId: get_collections
hidden: false
---