---
title: Roles and Permissions
excerpt: Use roles and permissions to define what actions users can take
deprecated: false
hidden: false
metadata:
  robots: index
---
Roles and permissions enable you define what users are allowed to do within an integration.

## Getting Started

Permissions determine what a user can and cannot do inside of LiveLike features. Permissions are granted to roles, which are then assigned to profiles within a given scope like the entire application or just a specific program. Once a role is assigned to a profile, that profile inherits all of its permissions.

* **Roles** are assigned to profiles and permission checks are performed against the authenticated profile's roles when they are performing some action. A profile can be assigned more than one role.
* **Permissions** represent an action a user can perform, like posting a comment or deleting a board. Permissions are granted to roles, and in effect a role is a named set of permissions. Once a role is assigned to a profile, that profile has all of that role's permissions.
* **Scopes** control which resources the role assignment is effective in. A role assignment is valid for one or more scopes.
* **Resources** are the entities that profiles act upon. Resources are things like Applications, Programs, Comment Boards, Chat Rooms, Chat Room Messages, and so on.

## Listing Available Roles

All available roles are available from the [Get List of Roles](ref:list-permissions) endpoint. Each role returned includes its name, ID, granted permissions, and relevant resource details.

## Assigning Roles

Roles must be assigned to profiles before they can take effect. To assign a role to a profile, use the Create Profile Role Assignment endpoint. For example, if you wanted to assign the Board Moderator role to all boards in your app `acme-app-id`, you use the application scope like this:

```javascript
LiveLike.createRoleAssignment({
  profileId: 'example-profile-id',
  roleId: 'example-role-id',
  scopes: [
    {
      resourceSlug: 'application',
      resourceId: 'acme-app-id'
    }
  ]
})
```

If you wanted to assign the board moderator role to only a single board and not every board in the app, you would use the comment board scope instead:

```javascript
LiveLike.createRoleAssignment({
  profileId: 'example-profile-id',
  roleId: 'example-role-id',
  scopes: [
    {
      resourceSlug: 'comment_board',
      resourceId: 'example-comment-board-id'
    }
  ]
})
```

## Listing Available Permissions

Use the [List Permissions](ref:list-permissions) endpoint to find the full set of permissions available to use in roles.

## Built-in Roles

> 🚧 Built-in roles will be changing soon
>
> An upcoming iteration of the RBAC system will no longer automatically create roles inside new applications. These built-in roles will continue to be listed here for historical reference.

| Role             | Slug               | Notes                                                                                               |
| :--------------- | :----------------- | :-------------------------------------------------------------------------------------------------- |
| Board Owner      | `board_owner`      | Profiles who create a comment board are automatically assigned the Board Owner role for that board. |
| Board Moderator  | `board_moderator`  |                                                                                                     |
| Widget Creator   | `widget_creator`   |                                                                                                     |
| Widget Publisher | `widget_publisher` |                                                                                                     |
