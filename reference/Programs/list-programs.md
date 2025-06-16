---
title: List Programs
excerpt: List all programs for an app
api:
  file: programs.json
  operationId: list-programs
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint returns the collection of all programs for a given application.
[block:callout]
{
  "type": "warning",
  "title": "Client ID parameter is required",
  "body": "The client_id query parameter must be provided when calling this endpoint. Leaving it out will cause an error response to be returned."
}
[/block]