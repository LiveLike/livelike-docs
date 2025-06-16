---
title: List Replies to Profile's Comments
excerpt: >-
  This API endpoint retrieves all replies made by other users to comments
  created by a specific profile. For example, if a profile named "ray" has
  created 10 comments, this API will list all the replies made to those 10
  comments by other users.
api:
  file: engagement-suite.json
  operationId: list-replies-to-profiles-comments
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Authentication

To access this API, you need to provide either:

1. A producer token.
2. The access token of the profile for which you want to retrieve replies (e.g., "ray's" access token).