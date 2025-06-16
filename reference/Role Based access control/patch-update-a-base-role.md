---
title: Patch Update a Base Role
excerpt: >-
  Used to add permissions, and update the key/name of the base role. Patch
  Update adds the supplied permissions to existing ones in the supplied base
  role.
api:
  file: engagement-suite.json
  operationId: patch-update-a-base-role
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
      slug: put-update-a-base-role
      title: Put Update a Base Role
---
> 📘 Producer Access Token Authentication is required to access this resource.

> 📘 Permission ids, keys and a role template key can be passed in the request body to create a base role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new base role.