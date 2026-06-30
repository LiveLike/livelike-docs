---
excerpt: ''
api:
  file: engagement-suite.json
  operationId: remove-members-from-group
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Add one of the following parameters:

* custom\_ids - list of custom id string of application profiles already created
* application\_profile\_ids - list of application profile id of application profiles already created

These application profiles will be removed from the group if they are already members; if not, they will be ignored.