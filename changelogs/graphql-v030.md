---
title: GraphQL v0.3.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-04-17T08:56:33.417Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Comment boards, RBAC, Poll votes and Rich posts. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Comment Board

***

* **commentBoard**: Get a specific comment board by ID.
* **commentBoards**: Get a list of comment boards.
* **createCommentBoard**: Create a new comment board by ID or Custom ID.
* **updateCommentBoard**: Update existing comment board by ID.
* **deleteCommentBoard**: Delete existing comment board by ID.

#### RBAC

***

* **permissions**: Get a list of system permission.
* **roles**: Get a list of roles.
* **rolesAssignment**: Get a list of roles assignment per profile.
* **createRole**: Create a new role.
* **createRoleAssignment**: Assign a role to given profile.

#### Profile

***

* **widgetsInteractions**: Get a list of user votes for text or image poll from given profile.

#### Poll

***

* **widgetsInteractions**: Get a list of user votes for text or image poll.

#### Program

***

* **widgets**: Get a ordered list of rich posts from given program.

#### Rich Post

***

* **widgets**: Get a ordered list of rich posts.