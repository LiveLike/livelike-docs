---
title: Comment Board Ban
excerpt: A tool for the moderators to ban users on a board.
deprecated: false
hidden: false
metadata:
  title: Comment Board Ban | Javascript SDK | LiveLike Developer Hub
  description: >-
    This document provides information on creating, listing, getting, and
    deleting comment board bans in an application, including the required
    parameters and API definitions for each action.
  robots: index
next:
  description: ''
---
## Create Comment Board Ban

Moderator can ban a profile

1. profile\_id: required, 
2. comment\_board\_id: optional, if not provided, the profile will be banned from all the comment boards in the application, provided the moderator has sufficient permissions to do that.
3. description: optional, this field can be used to provide additional information about a ban or the reason for banning a user.

**API Definition:** [createCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createCommentBoardBan)

```javascript
import { createCommentBoardBan } from "@livelike/javascript"

createCommentBoardBan({
  profileId: '<profile_id>',
  commentBoardId: '<comment_board_id>',
  description: '<Reason for banning>',
}).then((commentBoardBan) => console.log(commentBoardBan));
```

## List Comment Board Bans

Get a list of comment board bans in an Application. Each comment board ban resource represents restrictive access to the comment board for a given user profile.

1. As a producer or privileged user I can see all the comment-board-ban-profile from the application
2. As a moderator, I can get a list of all comment-board-ban-profile for the comment boards where I am a moderator
3. As a normal profile, I will get a list of comment-board-ban-profile for myself only.

**API Definition:** [getCommentBoardBans](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentBoardBans)

```javascript
import { getCommentBoardBans } from "@livelike/javascript"

getCommentBoardBans({
  profileId: '<profile_id>',
  commentBoardId: '<comment_board_id>',
}).then((paginatedResponse) => console.log(paginatedResponse));
```

## Get Comment Board Ban

Get Ban details by providing a ban id.

**API Definition:** [getCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentBoardBan)

```javascript
import { getCommentBoardBan } from "@livelike/javascript"

getCommentBoardBan({
  commentBoardBanId: '<comment_board_ban_id>',
}).then((commentBoardBan) => console.log(commentBoardBan));
```

## Delete Comment Board Ban

Remove a ban by providing a ban id.

**API Definition:** [deleteCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteCommentBoardBan)

```javascript
import { deleteCommentBoardBan } from "@livelike/javascript"

deleteCommentBoardBan({
  commentBoardBanId: '<comment_board_ban_id>',
})
```
