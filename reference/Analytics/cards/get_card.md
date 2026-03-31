---
title: Get Card Metadata
excerpt: >-
  Fetches the full metadata for a Card without executing the query. Use this
  endpoint to:


  - Inspect the Card's `parameters` array to understand what template-tag
  filters it accepts and whether they are required.

  - Read `result_metadata` to know the exact column names (use `display_name`)
  and data types of the output rows before downloading.

  - Check `query_type` (`"native"` vs `"query"`) and `display` to understand the
  Card's visualisation type.

  - Verify `fully_parameterized` — if `true`, you can call the download endpoint
  with `parameters: []`.


  > **Tip:** Always call this endpoint before your first download call to a new
  Card. The `display_name` values in `result_metadata` are the exact keys in
  JSON export rows.
api:
  file: analytics_schema.json
  operationId: get_card
hidden: false
---