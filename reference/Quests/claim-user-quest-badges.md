---
title: Claim User Quest Badge
excerpt: ''
api:
  file: engagement-suite.json
  operationId: claim-user-quest-badges
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Manually award badges to a user upon completing a quest:

- If claim_badges is not provided, all badges associated with the quest will be awarded.
- If claim_badges is provided, only the badges listed in it will be awarded, but only if they are valid and associated with the quest. Invalid or unrelated badges will be ignored.