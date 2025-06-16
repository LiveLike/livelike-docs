---
title: Create a Role
excerpt: ''
api:
  file: engagement-suite.json
  operationId: create-roles
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
      slug: get-roles
      title: Get List of Roles
    - type: endpoint
      slug: create-role-assignments
      title: Create Role Assignments
---
> 📘 Producer Access Token Authentication is required to access this resource.

> 📘 Permission ids, keys and a role template key can be passed in the request body to create a role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new role.
