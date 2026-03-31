---
title: Download Dashboard Card Data
excerpt: >-
  Executes the query for a specific Card embedded in a Dashboard and returns the
  results in the requested format. This is the correct endpoint to use when
  downloading data from a Card that is part of a Dashboard — it respects the
  Dashboard's parameter wiring.


  **Prerequisites:** Call `GET /api/dashboard/{dashboard_id}` first to retrieve:

  - `dashboard_id` — from `GET /api/collection/{id}/items`

  - `dashcard_id` — from `dashcards[].id` in the Dashboard response

  - `card_id` — from `dashcards[].card_id` in the Dashboard response


  **Applying dashboard-level filters:** If the Dashboard has `parameters` and
  you want to filter results, construct `QueryFilterParameter` entries using the
  `target` from the corresponding `parameter_mappings` on the Dashcard.
  Alternatively, you can also pass parameters directly targeting the Card's own
  template tags.


  **JSON format:** Returns a flat array of objects — keys are the `display_name`
  values from the Card's `result_metadata`.


  > **Note:** This endpoint uses `POST`, not `GET`, because filter parameters
  are passed in the request body.
api:
  file: analytics_schema.json
  operationId: post_dashboard_card_query_export
hidden: false
---