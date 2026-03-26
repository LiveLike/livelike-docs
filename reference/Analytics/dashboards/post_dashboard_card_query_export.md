---
title: Download Dashboard Card Data
excerpt: >-
  Downloads results from a card embedded in a dashboard. Call GET
  `/api/dashboard/{id}` first to obtain `dashcard_id` (`dashcards[].id`) and
  `card_id` (`dashcards[].card_id`).


  > **Note:** This is `POST` (not `GET`) because filter parameters are sent in
  the request body.
api:
  file: analytics_schema.json
  operationId: post_dashboard_card_query_export
hidden: false
---