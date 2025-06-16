---
title: Role Based Access Control
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
      slug: using-rbac
      title: Using RBAC
---
## Role Assignment

A role assignment has three components : 

1. Role to be assigned
2. Profile the role is assigned to
3. Scope of the assignment

A profile can have multiple role assignments, with different scopes for the same role as well to allow for access to multiple resource-instances of the same resource-kind.

> Resource object has two components : resource-kind (which is the kind of the resource, eg : chat-room), and resource-key (unique "id" of the resource). This is useful is defining the scope of the role. A resource-instance is an instance of a particular resource-kind. It is a resource object with a unique id. 
>
> See Scopes for more info : [examples](ref:role-based-access-control#scope)

> 📘 Role Assignment API : [Create Role Assignments](ref:create-role-assignments)

## Base Role

A Base Role defines a default set of permissions assigned to user profiles. It acts as the starting role for new users within an application.  
While multiple Base Roles can exist, only those marked as active are considered for assignment. This ensures new profiles receive the appropriate baseline access upon creation.

> 📘 Base Role Creation API: [Create a Base Role](ref:create-a-base-role)

### When does a Base Role apply?

Base roles are used to provide default permissions to profiles within an application.

When a base role is marked as active for an application, its permissions are automatically considered for any profile associated with that application. This means you do not need to manually assign a role to each new profile — as long as a base role is active, the associated permissions will be applied when access is evaluated.

This setup ensures a consistent baseline of access across all profiles in the application without requiring direct role assignments.

## Role

A role is a collection of permissions that can be assigned to a profile. Roles determine the level of access a profile has within the LiveLike application. Roles have to be explicitly assigned to a profile.

> 📘 Role Creation API : [Create a Role](ref:create-roles)

## Permissions

Permissions represent specific actions that profiles can execute within the LiveLike application. These actions are predefined and managed by LiveLike. Permissions only indicate what a profile can do, without specifying restrictions.

Below is a sample list of permissions provided by LiveLike, formatted by permission key and its description:

```Text Comment Board
delete-comment : Delete comment from a comment board	
delete-comment-board-ban : Delete comment board ban	
dismiss-reported-comment : Dismiss Reported Comment
view-comment-board-bans	: View Comment Board Bans	
view-reported-comments : View Reported Comments	
create-comment-board-ban	: Create comment board ban
```
```Text Widgets
create-alert : Create Alert
create-cheer-meter : Create Cheer Meter
create-emoji-poll : Create Emoji Poll
create-emoji-slider : Create Emoji Slider
create-image-number-prediction : Create Image Number Prediction
publish-text-ask : Publish Text Ask	
publish-text-poll : Publish Text Poll	
publish-text-prediction : Publish Text Prediction	
publish-text-prediction-follow-up : Publish Text Prediction Follow Up	
publish-text-quiz : Publish Text Quiz	
publish-twitter-spotlight : Publish Twitter Spotlight	
publish-video-alert	: Publish Video Alert	
```

> 📘 This API can be used to fetch the list of all permissions supported by livelike : [List Permissions](ref:list-permissions)

## Resource

Resources define distinct components or functionalities within the LiveLike application, which RBAC is applicable to. These components are predefined and are managed by LiveLike.

Below is a sample list of applicable resource-kinds provided by LiveLike:

```Text Resource Kinds
  chat-room
  profile
  comment-board
  twitter-spotlight
  social-embed
  rich-post
  program
```

> 📘 This API can be used to fetch all applicable resource-kinds : [Get List of Resources](ref:get-list-of-resources)

## Scope

Scope refers to the application-specific range of a resource category and a resource instance. It helps integrators precisely define the context in which a permission is applicable.  
It can be represented by a pair of resource-kind (type of resource), and resource-key (unique identifier of the resource, or "\*" for all resources of that kind)

### Example Scopes :

1. kind = program, key = program_a -> denotes a program with a particular id
2. kind = chat-room, key = "\*" -> denotes all chatrooms
3. kind = comment-board, key = board_a ; kind = comment-board, key = board_b -> denotes comment boards of id = a and b

## Role Template

Role templates are predefined sets of permissions designed for common use-cases. These templates are integrated into the system and are managed by LiveLike. However clients can use them to create a role with permissions associated with the role template.  
Here is an sample list of role templates and their respective permissions as provided by LiveLike:

```Text Widget Creator
create-alert
create-cheer-meter
create-emoji-poll
create-emoji-slider
create-image-number-prediction
create-image-number-prediction-follow-up
create-image-poll
create-image-prediction
create-image-prediction-follow-up
create-image-quiz
create-rich-post
create-social-embed
create-text-ask
create-text-poll
create-text-prediction
create-text-prediction-follow-up
create-text-quiz
create-twitter-spotlight
create-video-alert
```
```Text Widget Publisher
publish-alert
publish-cheer-meter
publish-emoji-poll
publish-emoji-slider
publish-image-number-prediction
publish-image-number-prediction-follow-up
publish-image-poll
publish-image-prediction
publish-image-prediction-follow-up
publish-image-quiz
publish-rich-post
publish-social-embed
publish-text-ask
publish-text-poll
publish-text-prediction
publish-text-prediction-follow-up
publish-text-quiz
publish-twitter-spotlight
publish-video-alert
```
```Text Comment Board Moderator
create-comment-board-ban  
view-comment-board-bans
delete-comment
delete-comment-board-ban
```

> 📘 This API can be used to get a list of all role templates offered by Livelike : [Get Role Templates](ref:get-role-templates)

## Role Assignment Examples:

1. Widget Creator role when assigned to a user A with scope of {kind, key = program, program_a}, would allow the user to create widgets in program_an only. 
2. Widget Creator role when assigned to a user B with scope of {kind, key = program, "\*"}, would allow the user to create widgets in all programs.
3. Another widget creator role assigned to user A with scope of {kind, key = program, program_b} would allow the user to create widgets in program_b along with program_a as well.