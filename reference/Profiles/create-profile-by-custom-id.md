---
title: Create Profile by Custom ID
excerpt: Create a new user profile with a custom ID
api:
  file: engagement-suite.json
  operationId: create-profile-by-custom-id
deprecated: false
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