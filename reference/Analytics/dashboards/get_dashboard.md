---
title: Get Dashboard
excerpt: >-
  Fetches full Dashboard metadata including all Dashcards and filter parameters.
  **Always call this endpoint before downloading data from a Dashboard-embedded
  Card** — you need the `dashcard_id` (`dashcards[].id`) and `card_id`
  (`dashcards[].card_id`) from this response to call the Dashboard Card Download
  endpoint.


  **What to look for in the response:**

  1. `dashcards` — iterate this array to find the Card you want by `card.name`.
  Extract `id` (dashcard_id) and `card_id`.

  2. `parameters` — dashboard-level filter definitions. If present, you can pass
  values for these in download requests to filter all wired Dashcards at once.

  3. `dashcards[].parameter_mappings` — shows exactly which dashboard filter
  maps to which template tag on each Card.

  4. `tabs` — if non-empty, the Dashboard has multiple tabs; Dashcards are
  distributed across tabs.
api:
  file: analytics_schema.json
  operationId: get_dashboard
hidden: false
---