---
title: Get Dashboard
excerpt: >-
  Returns full Dashboard metadata — all Dashcards, filter controls, and layout.
  Call this before downloading Dashboard Card data to get the `dashcard_id` and
  `card_id` you need.


  1. Find the Card you want in `dashcards[]` by `card.name`, then note its `id`
  (dashcard_id) and `card_id`.

  2. Check `parameters` — if filters exist, you can pass values in download
  requests.

  3. `dashcards[].parameter_mappings` shows which dashboard filter maps to which
  template tag on each Card.

  4. `tabs` — non-empty means the Dashboard has a tabbed layout.
api:
  file: livelike-analytics-api.json
  operationId: get_dashboard
hidden: false
---