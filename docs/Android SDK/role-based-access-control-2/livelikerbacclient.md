---
title: LiveLikeRBACClient
excerpt: LiveLikeRBACClient is an interface that manages user roles and permissions.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Working with LiveLikeRBACClient

* **Roles** are assigned to profiles and permission checks are performed against the authenticated profile's roles when they are performing some action. A profile can be assigned more than one role.
* **Permissions** represent an action a user can perform, like posting a comment or deleting a board. Permissions are granted to roles, and in effect a role is a named set of permissions. Once a role is assigned to a profile, that profile has all of that role's permissions.
* **Scopes** control which resources the role assignment is effective in. A role assignment is valid for one or more scopes.
* **Resources** are the entities that profiles act upon. Resources are things like Applications, Programs, Comment Boards, Chat Rooms, Chat Room Messages, and so on.

####

### Create a Role assignment

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
 rbac.createRoleAssignment(
                AssignRoleRequestOptions(profileId = "<profile-id>", roleKey = "<role-key>",
                    resourceKind = "<resource-kind>",
                    resourceKey = "<resource-key>")){ result, error ->
                error?.let {
                    //error
                }
                result?.let {assignedRoles ->
                    //assigned role
                }
            }
```

### Delete a Role assignment

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
  rbac.deleteRoleAssignment(UnAssignRoleRequestOptions("<assigned-role-id>")){result, error->
                //empty response
            }
```

### List assigned roles

```kotlin
 private var rbac: LiveLikeRBACClient
   rbac.getAssignedRoles(
                ListAssignedRoleRequestOptions(profileId = "<profile-id>"),
                LiveLikePagination.FIRST
            ){ result, error ->
                error?.let {
                      //error
                }
                result?.let {assignedRoles ->
                 //assigned roles list
                }
            }
```

### List Permissions

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
 rbac.getPermissions(LiveLikePagination.FIRST){result, error->
               result?.let{
                  //list of permissions
               }
               error?.let{
                   //errors
               }
            }
```

### List Roles

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
 rbac.getRoles(LiveLikePagination.FIRST){result, error->
               result?.let{
                  //list of roles
               }
               error?.let{
                   //errors
               }
            }
```

### List Resources

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
 rbac.getResources(LiveLikePagination.FIRST){result, error->
               result?.let{
                  //list of roles
               }
               error?.let{
                   //errors
               }
            }
```

### List Scopes

<br />

```kotlin
 private var rbac: LiveLikeRBACClient
 rbac.getScopes(ListScopesRequest(resourceId = "<resource-id>"),
                LiveLikePagination.FIRST){ result, error->
               result?.let{
                  //
               }
               error?.let{

               }
            }
```
