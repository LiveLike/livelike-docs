---
title: Download Card Data
excerpt: >-
  Runs the Card's query and returns the results in the format you choose —
  `csv`, `json`, or `xlsx`.


  **Before calling this:** Check `fully_parameterized` on the Card. If it is
  `false`, call `GET /api/card/{id}` first and look for parameters where
  `required: true` and `default` is not set — you must include those in the
  request body or this call will fail.


  **Request body:** Pass a `parameters` array with one entry per filter slot you
  want to set. Pass an empty array `[]` if there are no required filters or you
  want the defaults.


  **JSON format:** Returns a flat array of objects. Each object is one row, and
  the keys are the `display_name` values from `result_metadata`.


  **Picking a format:**

  | Format | Best for |

  |--------|----------|

  | `json` | Processing results in code |

  | `csv`  | Spreadsheets or data pipelines |

  | `xlsx` | Formatted Excel files for end users |


  > **Note:** This endpoint is a `POST`, not a `GET`, because filter values go
  in the request body — not the URL.
api:
  file: livelike-analytics-api.json
  operationId: post_card_query_export
hidden: false
---