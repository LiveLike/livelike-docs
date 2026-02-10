---
title: Profile permissions check
excerpt: >-
  To check if a profile has specific permissions in the given scopes or
  resources 
api:
  file: engagement-suite.json
  operationId: get_profiles{ProfileUUID}permissions-check
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
User can provide mix of `scope_id` AND/OR (`resource_kind` + `resource_key`) combination. 

Parameters can be repeated to support bulk or multiple permission checks in a single request.
Examples

```shell
# Check single permission against specific scope
GET /?permission_key=send-message&scope_id=scope-uuid-123

# Check multiple permissions against specific scope
GET /?permission_key=send-message&permission_key=delete-message&scope_id=scope-uuid-123

# Check multiple permissions against multiple scope
GET /?permission_key=send-message&permission_key=delete-message&scope_id=scope-uuid-123&scope_id=scope-uuid-456

# Check permissions against resource kind/key (includes wildcard support)
GET /?permission_key=send-message&resource_kind=chat-room&resource_key=uuid-456

# Check multiple permissions against multiple resources
GET /?permission_key=send-message&permission_key=moderate&resource_kind=chat-room&resource_key=uuid-123&resource_key=uuid-456
```

<br />

**Validation:**

* `permission_key` is required
* Must provide either `scope_id` AND/OR (`resource_kind` + `resource_key`)
* `scope_id`  and/or `resource_key`  must be a valid UUID.

If a user violates any of these rules, an HTTP 400 response with an appropriate error message will be returned.

The response includes a `results` list. Each object in the list contains the user-provided permission and scope details, along with a `has_permission` flag indicating whether the profile has that permission within the given scope.

<br />