---
title: Role Grants
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Role Grants allow roles to be assigned to a grantee (currently a **Profile Group**) instead of individual Profiles.

When a role is granted to a Profile Group:

- All existing members inherit the role automatically.
- New members inherit the role when they join the group.
- Members automatically lose the inherited role when they leave the group.
- Removing a role grant revokes only that grant. Roles assigned through other sources remain unaffected.

## Functional Behavior

### Assign Role

- Assign a role to a Profile Group.
- Current members receive the role immediately.
- Future members inherit the role automatically.
- Supports both global-scoped and entity-scoped role grants.
- Each role grant is audited.

### Remove Role

- Remove a role grant from a Profile Group.
- Members retain the role if it is also assigned directly or inherited from another grantee.
- Removing a role grant does not modify any linked entities.
- Each removal is audited.

### Permission Evaluation

A Profile's permissions are evaluated from both sources:

1. Direct role assignments.
2. Role grants inherited through grantee membership.

A permission is granted if either source provides the required role.

## Edge Cases

- Role grants remain valid even when a Profile Group has no members. Future members automatically inherit the role.
- If a Profile Group is deactivated or deleted, its inherited grants become inactive.
- Assigning or removing a role grant is a single operation regardless of group size. No per-member role assignments are created.

***

# API Endpoints

| Method | Use                     | Endpoint                                               |
| ------ | ----------------------- | ------------------------------------------------------ |
| POST   | Assign                  | `/api/v1/role-grants/`                                 |
| GET    | List                    | `/api/v1/role-grants/`                                 |
| GET    | Detail                  | `/api/v1/role-grants/{grant_uuid}/`                    |
| DELETE | Unassign by grant ID    | `/api/v1/role-grants/{grant_uuid}/`                    |
| POST   | Unassign by Natual keys | `/api/v1/applications/{client_id}/revoke-role-grants/` |

<br />
