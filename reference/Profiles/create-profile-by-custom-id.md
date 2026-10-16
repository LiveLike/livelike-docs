---
api:
  file: engagement-suite.json
  operationId: create-profile-by-custom-id
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
A custom ID must be unique inside an application.

This endpoint will return a 201 status code if the custom ID is not in use and a new profile is created. If the custom ID is already in use it will return a 409 status code instead.