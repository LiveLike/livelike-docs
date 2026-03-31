---
title: Download Dashboard Card Data
excerpt: >-
  Runs the query for a specific Card inside a Dashboard and returns the results
  in the format you choose. Use this endpoint — rather than the standalone Card
  download — when the Card is part of a Dashboard, since it respects the
  Dashboard's filter wiring.


  **Before you call this, you need three IDs from `GET
  /api/dashboard/{dashboard_id}`:**

  - `dashboard_id` — from `GET /api/collection/{id}/items`

  - `dashcard_id` — from `dashcards[].id` in the Dashboard response

  - `card_id` — from `dashcards[].card_id` in the Dashboard response


  **Applying dashboard filters:** If the Dashboard has `parameters`, build
  `QueryFilterParameter` entries using the `target` from the Dashcard's
  `parameter_mappings`. You can also target the Card's own template tags
  directly.


  **JSON format:** Returns a flat array of objects — keys are the `display_name`
  values from the Card's `result_metadata`.


  > **Note:** This endpoint is a `POST`, not a `GET`, because filter values go
  in the request body.
api:
  file: livelike-analytics-api.json
  operationId: post_dashboard_card_query_export
hidden: false
---