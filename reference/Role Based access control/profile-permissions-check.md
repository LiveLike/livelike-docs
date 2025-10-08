---
title: Profile permissions check
excerpt: >-
  To check if a profile has specific permissions in the given scopes or
  resources 
api:
  file: engagement-suite.json
  operationId: get_profiles{ProfileUUID}permissions-check
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
**Validation:**

* `permission_key` is required
* Must provide either `scope_id` AND/OR (`resource_kind` + `resource_key`)
* `scope_id`  and/or `resource_key`  must be a valid UUID.

If a user violates any of these rules, an HTTP 400 response with an appropriate error message will be returned.

The response includes a `results` list. Each object in the list contains the user-provided permission and scope details, along with a `has_permission` flag indicating whether the profile has that permission within the given scope.

<br />