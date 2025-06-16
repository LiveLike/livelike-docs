---
title: Patch Update a Role
excerpt: >-
  Used to add permissions, and update the key/name of the role. Patch Update
  adds the supplied permissions to existing ones in the supplied role.
api:
  file: engagement-suite.json
  operationId: update-a-role
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: endpoint
      slug: patch-update-a-role-copy
      title: Put Update a Role
---
> 📘 Producer Access Token Authentication is required to access this resource.

> 📘 Permission ids, keys and a role template key can be passed in the request body to create a role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new role.