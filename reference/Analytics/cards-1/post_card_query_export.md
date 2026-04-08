---
title: Download Card Data
excerpt: >-
  Downloads the report data. Choose `csv`, `json`, or `xlsx` depending on what
  you need.


  If the report has no required filters, pass `parameters: []`. If it does,
  include a `QueryFilterParameter` entry for each required filter.


  > This is a `POST` request — filters go in the request body, not the URL.
api:
  file: livelike-analytics-api.json
  operationId: post_card_query_export
hidden: false
---