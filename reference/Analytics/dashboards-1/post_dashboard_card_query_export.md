---
title: Download Dashboard Card Data
excerpt: >-
  Runs the query for a specific Card inside a Dashboard and returns results in
  the format you choose. Use this instead of the standalone Card download when
  the Card is on a Dashboard — it respects the Dashboard's filter wiring.


  You need three IDs from `GET /api/dashboard/{dashboard_id}`:

  - `dashboard_id` — from `GET /api/collection/{id}/items`

  - `dashcard_id` — from `dashcards[].id`

  - `card_id` — from `dashcards[].card_id`


  To apply dashboard filters, build `QueryFilterParameter` entries using the
  `target` from the Dashcard's `parameter_mappings`.


  > This is a `POST`, not a `GET` — filter values go in the request body.
api:
  file: livelike-analytics-api.json
  operationId: post_dashboard_card_query_export
hidden: false
---