---
title: Remove Members from Group
excerpt: ''
api:
  file: engagement-suite.json
  operationId: remove-members-from-group
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Add one of the following parameters:

- custom_ids - list of custom id string of application profiles already created
- application_profile_ids - list of application profile id of application profiles already created

These application profiles will be removed from the group if they are already members; if not, they will be ignored.