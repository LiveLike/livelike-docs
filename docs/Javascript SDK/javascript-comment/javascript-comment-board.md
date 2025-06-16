---
title: Board
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
A resource that represents a topic to comment on. Clients associate boards with their blog posts, videos, teams, individual sports matches, and so on.

For example, a board may be created for a specific blog post, allowing readers to share their thoughts, questions, and opinions about the topic. Similarly, a board may be associated with a particular video, providing viewers with a platform to discuss the content and engage with each other.

Boards can be used in a variety of contexts, including online communities, social media platforms, and content-sharing websites. They allow individuals to connect and communicate with others who share similar interests, allowing for the exchange of ideas, feedback, and knowledge.

Overall, a board is a valuable resource for fostering engagement and facilitating communication among individuals who are interested in a particular topic or content.

## Creating a Comment Board

Users can create a Comment Board using the `createCommentBoard` method.

**API Definition** : [createCommentBoard]((https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createCommentBoard))

```javascript
import { createCommentBoard } from '@livelike/javascript'

createCommentBoard({
  title: 'sd',
  customId: 'postid1',
  repliesDepth: 2,
  allowComments: true,
  description: 'desc',
  customData: 'abc',
}).then((commentBoard) => console.log(commentBoard));
```



## Updating a Comment Board

**API Definition** : [updateCommentBoard]((https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=updateCommentBoard))

```javascript
import { updateCommentBoard } from '@livelike/javascript'

updateCommentBoard({
  commentBoardId: '<comment-board-id>',
  title: 'title',
  customId: 'postID431',
  repliesDepth: 1,
  allowComments: true,
  description: 'abc',
  customData: 'custom data',
}).then((commentBoard) => console.log(commentBoard));
```



## Getting a list of Comments Boards

**API Definition** : [getCommentBoards]((https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentBoards))

```javascript
import { getCommentBoards } from '@livelike/javascript'

getCommentBoards().then(({results}) => console.log(results))
```



## Deleting a Comment Board

**API Definition** : [deleteCommentBoard]((https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteCommentBoard))

```javascript
import { deleteCommentBoard } from '@livelike/javascript'

deleteCommentBoard({
  commentBoardId: '<comment-board-id>',
}).then(({ results }) => console.log(results));
```