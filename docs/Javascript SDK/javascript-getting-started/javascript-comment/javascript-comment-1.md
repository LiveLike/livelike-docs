---
title: Comment
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
## Creating a Comment

An "addComment" API would likely be used to create a new comment on a particular comment board or thread. The function takes in several parameters, including the text of the comment, any custom data to be included with the comment, and the ID of the comment board where the comment should be posted. The function returns a promise that resolves with the new comment object, which can then be logged to the console or used in further code.

**API Definition**: [addComment](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addComment)

```javascript
import { addComment } from '@livelike/javascript'

addComment({
     text: '<Your text comment>',
     customData:'<Your custom data to send with reply comment>',
     commentBoardId:'<Your comment board Id>'
   }).then(comment => console.log(comment));
```

## Get a list of Top Level Comments

A "getComments" API would likely be used to retrieve comments from a particular comment board. The function takes in several parameters, including the ID of the comment board, a sorting parameter to control the order of the returned comments, and optional parameters to filter comments by their reply timestamps. The function returns a promise that resolves with an object representing the comment board, including an array of the retrieved comments.

**commentBoardId**: This parameter is a required string value that specifies the ID of the comment board from which to retrieve comments.

**sorting**: This parameter is an optional string value that specifies the sorting order of the returned comments. This value is typically an enum or set of pre-defined values that control the order based on criteria such as date, popularity, or relevance.

**repliedSince**: This parameter is an optional string value that specifies the earliest timestamp for retrieved comments, filtered by the comment reply timestamp. It should be a valid date-time string in ISO 8601 format.

**repliedUntil**: This parameter is an optional string value that specifies the latest timestamp for retrieved comments, filtered by the comment reply timestamp. It should also be a valid date-time string in ISO 8601 format.

**isReported**: This parameter is an optional boolean value that specifies whether the comment is reported or not.

**API Definition**: [getComments](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getComments)

```javascript
import { getComments } from '@livelike/javascript'

getComments({
     commentBoardId:'<comment-board-id>',
     sorting:'<Your comment sorting enum value>',
     repliedSince:'<2023-12-19T15:28:46.493Z>',
     repliedUntil:'<2023-12-19T15:28:46.493Z>',
  	 isReported: true,
  }).then(padinatedResponse => console.log(padinatedResponse));
```

## Edit a Comment

An "editComment" API would likely be used to update the text or custom data of an existing comment on a particular comment board or thread. The function takes in several parameters, including the ID of the comment board and the ID of the comment to be updated, as well as the new text and custom data values. The function returns a promise that resolves with the updated comment object, which can then be logged to the console or used in further code.

**commentBoardId**: This parameter is a required string value that specifies the ID of the comment board on which the comment to be edited exists.

**commentId**: This parameter is a required string value that specifies the ID of the comment to be edited.

**text**: This parameter is an optional string value that specifies the new text for the updated comment.

**customData**: This parameter is an optional string value that specifies any new custom data to be associated with the updated comment.

**API Definition**: [editComment](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=editComment)

```javascript
import { editComment } from '@livelike/javascript'

editComment({
   commentBoardId: "<comment-board-id>",
   commentId: "<comment-id>",
   text: '<Your text comment>',
   customData: '<Your custom data to send with reply comment>',
  }).then(comment => console.log(comment))
```

## Delete a Comment

A "deleteComment" API would likely be used to delete an existing comment on a particular comment board or thread. The function takes in several parameters, including the ID of the comment board and the ID of the comment to be deleted. The function does not typically return anything but may throw an error if the deletion fails for some reason.

**API Definition**: [deleteComment](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteComment)

```javascript
import { deleteComment } from '@livelike/javascript'

deleteComment({
   commentBoardId: "<comment-board-id>",
   commentId: "<comment-id>"
  })
```

## Get a Comment Details

A "getComment" API would likely be used to retrieve a single comment object based on its ID and the ID of the comment board on which it exists. The function takes in two parameters, including the ID of the comment board and the ID of the comment being requested. The function returns a promise that resolves with the requested comment object.

**API Definition**: [getComment](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getComment)

```javascript
import { getComment } from '@livelike/javascript'

  getComment({
   commentBoardId: "<comment-board-id>",
   commentId:"<comment-id>"})
  .then(({results}) => console.log(results))
```
