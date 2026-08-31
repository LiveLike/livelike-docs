---
title: GraphQL v0.4.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-04-26T15:42:37.046Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Application, Comment, Rich Post. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Application

***

* **application**: Get a specific application by client ID.

#### Comment

***

* **comment**: Get a specific comment by ID.
* **comments**: Get all top level comments for a comment board.
* **commentReplies**: Get all replies for a comment.
* **createComment**: Create a comment for comment board.
* **createCommentReply**: Create a reply for comment.

#### Rich Post

***

* **createRichPost**: Create a rich post.

#### Widget

***

* **publishWidget** : Publish available widget, extend for RichPost publish.