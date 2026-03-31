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
  `parameters: []` and it'll work.


  > **Tip:** The `display_name` values in `result_metadata` are the exact keys
  in JSON export rows.
api:
  file: livelike-analytics-api.json
  operationId: get_card
hidden: false
---