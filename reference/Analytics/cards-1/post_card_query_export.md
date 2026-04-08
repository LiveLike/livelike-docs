---
title: Download Card Data
excerpt: >-
  Runs the Card's query and returns results in the format you choose.


  Check `fully_parameterized` first. If `false`, call `GET /api/card/{id}` and
  look for `required: true` parameters with no `default` — you must include
  those in the request body.


  **Request body:** `parameters` array with one entry per filter you want to
  set. Pass `[]` if there are no required filters.


  **JSON format:** flat array of objects — keys are `display_name` values from
  `result_metadata`.


  | Format | Use for |

  |--------|----------|

  | `json` | Processing in code |

  | `csv` | Spreadsheets or pipelines |

  | `xlsx` | Excel files for end users |


  > This is a `POST`, not a `GET` — filter values go in the request body.
api:
  file: livelike-analytics-api.json
  operationId: post_card_query_export
hidden: false
---