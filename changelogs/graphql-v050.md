---
title: GraphQL v0.5.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-04-30T15:38:25.915Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Comment and Chat Room. Below is a structured documentation to outline these changes:

***

### Release Changes

#### ChatRoom

***

* **chatRoom**: Get a specific chat room by ID.
* **chatRooms**: Get all chat rooms related to application.
* **createChatRoom**: Create a chat room.
* **updateChatRoom**: Update a chat room.
* **deleteChatRoom**: Delete a chat room.

#### Comment

***

* **commentReport**: Get a specific comment report by ID.
* **commentReports**: Get all comments reports for given comment ID or comment board ID.
* **createCommentReport**: Report given comment by ID.
* **dismissCommentReport**: Dismiss given comment report by ID.

 Type **Comment** is extended to contain type **Author(Profile)** data.