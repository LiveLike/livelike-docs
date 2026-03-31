---
title: Get Collection Tree
excerpt: >-
  Returns the full Collection hierarchy as a nested tree. Each Collection
  includes a `children` array with its sub-collections, all the way down. This
  saves you from having to call `/api/collection/` and manually reconstructing
  the tree from `location` paths.


  **When to use:** Reach for this endpoint when building navigation, discovering
  nested client sub-folders, or walking the full hierarchy to find a deeply
  nested Collection by name.


  > **Tip:** The `entity_id` field stays stable across renames and moves — it's
  safer to store than `id` or `slug`.
api:
  file: livelike-analytics-api.json
  operationId: get_collection_tree
hidden: false
---