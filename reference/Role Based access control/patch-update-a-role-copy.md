---
title: Put Update a Role
excerpt: >-
  Used to replace existing permissions in a role to a new set of permissions,
  and also update name/key of the role
api:
  file: engagement-suite.json
  operationId: patch-update-a-role-copy
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
      slug: delete-a-role
      title: Delete a Role
---
> 📘 PUT Update replaces existing permissions in a role, and adds the set of all supplied permissions to the role.
>
> > 📘 Permission ids, keys and a role template key can be passed in the request body to create a role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new role.

> 📘 Producer Access Token Authentication is required to access this resource.
