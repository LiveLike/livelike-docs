---
title: Replies
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
## Reply to a Comment

An "addCommentReply" API would likely be used to add a new comment as a reply to an existing comment on a particular comment board or thread. The function takes in several parameters, including the ID of the comment board and the ID of the parent comment to which the new reply will be added, as well as the text and custom data values for the new reply. The function returns a promise that resolves with the newly created comment object, which can then be logged to the console or used in further code.

**text**: This parameter is a required string value that specifies the text content of the new comment reply.

**customData**: This parameter is an optional string value that specifies any custom data to be associated with the new comment reply.

**commentBoardId**: This parameter is a required string value that specifies the ID of the comment board on which the parent comment and new reply exist.

**parentCommentId**: This parameter is a required string value that specifies the ID of the parent comment to which the new reply will be added as a child.

**API Definition**: [addCommentReply](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addCommentReply)

```javascript
import { addCommentReply } from '@livelike/javascript'

addCommentReply({
     text: '<Your text comment>',
     customData: '<Your custom data to send with reply comment>',
     commentBoardId: '<Your comment board Id>',
     parentCommentId: '<Your parent  comment Id>'
}).then(comment => console.log(comment));
```



## List of comments replies

A "getCommentReplies" API would likely be used to retrieve all the replies to a specific comment on a particular comment board or thread. The function takes in several parameters, including the ID of the comment board and the ID of the comment for which replies are being requested, as well as a sorting value that determines the order in which replies will be returned. The function returns a promise that resolves with an array of comment objects representing each of the replies.

**commentBoardId**: This parameter is a required string value that specifies the ID of the comment board on which the comment and its replies exist.

**commentId**: This parameter is a required string value that specifies the ID of the comment for which replies are being requested.

**sorting**: This parameter is an optional value that determines the order in which replies will be returned. The possible values for this parameter will depend on the specific API being used, but in this case, it appears that the CommentSort.NEWEST value is being used to sort replies in descending order based on their creation date (i.e., newest replies first).

**API Definition**: [getCommentReplies](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentReplies)



```javascript
import { getCommentReplies } from '@livelike/javascript'

getCommentReplies({
     commentBoardId:'<comment-board-id>',
     commentId:'<comment-id>',
     sorting: CommentSort.NEWEST,
  }).then(comments => console.log(comments));
```