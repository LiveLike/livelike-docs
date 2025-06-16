---
title: List Badge progress
excerpt: ''
api:
  file: engagement-suite.json
  operationId: list-badge-progress
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Returns the progress that has been made by a profile toward earning the requested badges. Only badges that have a reward item threshold configured can have progress made towards them.

Progress for multiple badges can be requested together by repeating the `badge_id` parameter once for each badge.