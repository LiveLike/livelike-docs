---
title: Using RBAC
excerpt: ''
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
      slug: list-permissions
      title: List Permissions
---
# How to integrate RBAC into your systems

## Model your roles and permissions

LiveLike's [Permissions API](ref:list-permissions) and [Role Templates API](ref:get-role-templates) provide exhaustive lists of permissions and role-templates which can be used to tackle some standard use-cases, eg : a comments-board-moderator, or a widget-creator role. 

For more custom requirements, integrators can choose what specific permissions they want to add to a role. Eg : a global widgets and comments moderator role can have a permission set of both comments-moderator, and a widget-moderator role.

## Create your modeled roles

After finalizing required roles and permissions, [Role Creation API](ref:create-roles) is used to then create a role out of the permissions/role-templates for the integrator's application.

## Assign created roles to your users

Refer [Create Role Assignment API](ref:create-role-assignments) for details on usage.