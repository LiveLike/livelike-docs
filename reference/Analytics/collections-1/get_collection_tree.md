---
title: Get Collection Tree
excerpt: >-
  Returns the full Collection hierarchy as a nested tree. Each Collection has a
  `children` array containing its sub-collections recursively.


  Useful for building navigation or finding a deeply nested Collection by name
  without having to reconstruct the tree from `location` paths.


  > **Tip:** `entity_id` stays stable across renames and moves — safer to store
  than `id` or `slug`.
api:
  file: livelike-analytics-api.json
  operationId: get_collection_tree
hidden: false
---