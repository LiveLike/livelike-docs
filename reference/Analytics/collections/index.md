---
title: Collections
excerpt: >-
  Collections are the top-level organisational unit in LiveLike Analytics. They
  act as folders that can hold Cards (saved queries), Dashboards, and Documents,
  and they can be nested arbitrarily deep to reflect your team's structure or
  client hierarchy.
hidden: false
---
**Key facts:**

* Every Card and Dashboard belongs to exactly one Collection.
* The root Collection has the special id `\"root\"` (a string, not an integer).
* The `location` field encodes the full ancestry path, e.g. `\"/11/74/\"` means the Collection lives inside Collection 74, which lives inside Collection 11.
*  Your API key's access is scoped: you will only see Collections (and their contents) that have been explicitly shared with your key.\n- Use `GET /api/collection/tree` to get the entire visible hierarchy in one call; use `GET /api/collection/` to get a flat list; use `GET /api/collection/{id}/items` to list the contents of a specific Collection.

<br />
