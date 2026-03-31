---
title: Get Collection Tree
excerpt: >-
  Returns the full Collection hierarchy visible to your API key as a nested
  tree. Each Collection object includes a `children` array of its direct
  sub-collections, recursively. This is more efficient than calling `GET
  /api/collection/` and manually reconstructing the hierarchy from `location`
  paths.


  **When to use:** Use this endpoint when building navigation UIs, discovering
  nested client sub-collections, or programmatically walking the full hierarchy
  to find a deeply-nested Collection by name.


  > **Tip:** The `entity_id` field is stable across renames and moves — prefer
  it over `id` or `slug` when storing references.
api:
  file: analytics_schema.json
  operationId: get_collection_tree
hidden: false
---