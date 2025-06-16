---
title: Add Badges to Quest
excerpt: ''
api:
  file: engagement-suite.json
  operationId: add-quest-badges
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
- The Quest and Badges need to be created before establishing any links between them. 
- A list of Badge IDs is provided, which will be associated with the Quest. 
- Any invalid badge will be skipped from being added. 
- Adding the same badge repeatedly will not result in multiple additions; the process is idempotent. 
- There is a limit to the number of badges that can be linked to a Quest; exceeding this limit will result in an error.