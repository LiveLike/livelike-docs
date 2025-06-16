---
title: Create a Base Role
excerpt: ''
api:
  file: engagement-suite.json
  operationId: create-a-base-role
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
      slug: get-list-of-base-roles
      title: Get List of Base Roles
    - type: endpoint
      slug: create-role-assignments
      title: Create Role Assignments
---
> 📘 Producer Access Token Authentication is required to access this resource.

> 📘 Permission ids, keys and a role template key can be passed in the request body to create a base role. A union set of the permissions represented by these keys, including permissions in the role template, are added to the new base role.
