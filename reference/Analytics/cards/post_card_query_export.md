---
title: Download Card Data
excerpt: >-
  Executes the Card's query and returns the results in the requested format.
  Supports `csv`, `json`, and `xlsx`.


  **Request body:** Pass a `parameters` array to filter the results. Each entry
  targets one template tag on the Card. Pass an empty array `[]` if no filters
  are needed (or all tags have defaults).


  **JSON format:** Returns a flat array of objects. Each object represents one
  row; keys are the `display_name` values from `result_metadata`.


  **Choosing an export format:**

  | Format | Use when… |

  |--------|-----------|

  | `json` | You need to process results programmatically in code |

  | `csv`  | You want a lightweight flat file for spreadsheets or data pipelines
  |

  | `xlsx` | You need a formatted Excel file for end-user consumption |


  > **Note:** This endpoint uses `POST`, not `GET`, because filter parameters
  are passed in the request body — not as query string parameters.
api:
  file: analytics_schema.json
  operationId: post_card_query_export
hidden: false
---