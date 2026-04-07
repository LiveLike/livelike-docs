---
title: Get Card Metadata
excerpt: >-
  Gets the full metadata for a Card without actually running the query. Call
  this first to understand what you're working with before hitting the download
  endpoint.


  **What you'll learn from this:**

  - `parameters` — what filter slots exist and whether they're required.

  - `result_metadata` — the exact column names (use `display_name`) and data
  types of the output before you download.

  - `query_type` and `display` — how the Card was built and what chart type it
  uses.

  - `fully_parameterized` — if `true`, you can call the download endpoint with
  `parameters: []` and it'll work. If `false`, check `parameters[]` for entries
  where `required: true` and `default` is absent — you must pass values for
  those or the download will fail with a `400` or `500`.


  > **Tip:** The `display_name` values in `result_metadata` are the exact keys
  in JSON export rows.
api:
  file: livelike-analytics-api.json
  operationId: get_card
hidden: false
---