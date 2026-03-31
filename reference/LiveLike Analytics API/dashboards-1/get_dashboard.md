---
title: Get Dashboard
excerpt: >-
  Gets full Dashboard metadata — all Dashcards, filter controls, and layout
  info. **Call this before downloading data from a Dashboard Card** — you need
  the `dashcard_id` (`dashcards[].id`) and `card_id` (`dashcards[].card_id`)
  from this response.


  **What to look for in the response:**

  1. `dashcards` — find the Card you want by `card.name`, then grab its `id`
  (dashcard_id) and `card_id`.

  2. `parameters` — if the Dashboard has filters, you can pass values for them
  in download requests to filter all wired Dashcards at once.

  3. `dashcards[].parameter_mappings` — shows exactly which dashboard filter
  connects to which template tag on each Card.

  4. `tabs` — if non-empty, the Dashboard uses tabs and Dashcards are spread
  across them.
api:
  file: livelike-analytics-api.json
  operationId: get_dashboard
hidden: false
---