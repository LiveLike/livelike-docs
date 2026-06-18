---
excerpt: ''
api:
  file: engagement-suite.json
  operationId: create-a-profile-block
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Rules:

* Allow blocking a profile using either Profile ID (UUID) or Profile Custom ID.
* Exactly one of these must be provided. Supplying both is invalid.
* The provided Profile ID or Custom ID must belong to the same application as the blocker (based on the auth token). If not, return HTTP 400 with the message "**Blocked profile not found"**.
* If a block relationship already exists between the two users, return HTTP 409.