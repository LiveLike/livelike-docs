---
api:
  file: engagement-suite.json
  operationId: reward-item-transfers
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint is used to transfer reward items from one user to another. The `profile_id` in the URL is the sender, and the `recipient_profile_id` in the body is the recipient. Requires Producer Token or User Access Token associated with the sender's profile.