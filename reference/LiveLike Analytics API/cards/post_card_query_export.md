---
title: Download Card Data
excerpt: >-
  Downloads card results as CSV, JSON, or XLSX. Pass an empty `parameters` array
  if no filters are needed. The JSON format returns a flat array of row objects
  — keys are column display names.


  > **Note:** This is `POST` (not `GET`) because filter parameters are sent in
  the request body.
api:
  file: analytics_schema.json
  operationId: post_card_query_export
hidden: false
---