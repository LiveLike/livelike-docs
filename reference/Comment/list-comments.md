---
title: List comments
excerpt: ''
api:
  file: engagement-suite.json
  operationId: list-comments
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Comments with reaction counts

This API also returns the count of user reactions to each comment, given that the comment board has a reaction space attached to it.

## Trending comments

Each comment has a `trending_score` property that is based on a combination of factors like recency, reply count, and reaction count. A higher score indicates a higher-ranked comment. Use the `ordering=trending_score` parameter to order comments by trending score descending.