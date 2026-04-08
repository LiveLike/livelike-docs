---
title: Get Card Metadata
excerpt: >-
  Returns the full metadata for a Card without running the query. Call this
  before downloading to check what filters are needed and what columns come
  back.


  - `parameters` — filter slots and whether they're required.

  - `result_metadata` — output columns; use `display_name` as the key in JSON
  exports.

  - `fully_parameterized` — `true` means you can call the download endpoint with
  `parameters: []`. If `false`, check `parameters[]` for entries where
  `required: true` and no `default` — those must be passed or the download
  fails.


  > **Tip:** `display_name` values in `result_metadata` are the exact keys in
  JSON export rows.
api:
  file: livelike-analytics-api.json
  operationId: get_card
hidden: false
---