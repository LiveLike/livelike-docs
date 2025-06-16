---
title: Put Update a Base Role
excerpt: >-
  Used to replace existing permissions in a base role to a new set of
  permissions, and also update name/key of the base role
api:
  file: engagement-suite.json
  operationId: put-update-a-base-role
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
      slug: delete-a-base-role
      title: Delete a Base Role
---
> 📘 PUT Update replaces existing permissions in a base role, and adds the set of all supplied permissions to the base role.
> 
> > 📘 Permission ids, keys and a role template key can be passed in the request body to create a base role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new base role.

> 📘 Producer Access Token Authentication is required to access this resource.