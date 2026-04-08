---
title: Get Card Metadata
excerpt: >-
  Returns the details of a report — what columns it has and whether any filters
  are required.


  Check `fully_parameterized` before downloading. If it's `true`, you can
  download straight away with `parameters: []`. If it's `false`, look through
  `parameters` for any entry where `required` is `true` — you'll need to pass a
  value for those.
api:
  file: livelike-analytics-api.json
  operationId: get_card
hidden: false
---