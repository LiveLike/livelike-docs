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
[block:api-header]
{
  "title": "Create Comment Board Ban"
}
[/block]
Moderator can ban a profile
1. profile_id: required, 
2. comment_board_id: optional, if not provided, the profile will be banned from all the comment boards in the application, provided the moderator has sufficient permissions to do that.
3. description: optional, this field can be used to provide additional information about a ban or the reason for banning a user.

**API Definition:** [createCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createCommentBoardBan)
[block:code]
{
  "codes": [
    {
      "code": "import { createCommentBoardBan } from \"@livelike/javascript\"\n\ncreateCommentBoardBan({\n  profileId: '<profile_id>',\n  commentBoardId: '<comment_board_id>',\n  description: '<Reason for banning>',\n}).then((commentBoardBan) => console.log(commentBoardBan));",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "List Comment Board Bans"
}
[/block]
Get a list of comment board bans in an Application. Each comment board ban resource represents restrictive access to the comment board for a given user profile.

1. As a producer or privileged user I can see all the comment-board-ban-profile from the application
2. As a moderator, I can get a list of all comment-board-ban-profile for the comment boards where I am a moderator
3. As a normal profile, I will get a list of comment-board-ban-profile for myself only.

**API Definition:** [getCommentBoardBans](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentBoardBans)
[block:code]
{
  "codes": [
    {
      "code": "import { getCommentBoardBans } from \"@livelike/javascript\"\n\ngetCommentBoardBans({\n  profileId: '<profile_id>',\n  commentBoardId: '<comment_board_id>',\n}).then((paginatedResponse) => console.log(paginatedResponse));",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Comment Board Ban"
}
[/block]
Get Ban details by providing a ban id.

**API Definition:** [getCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentBoardBan)
[block:code]
{
  "codes": [
    {
      "code": "import { getCommentBoardBan } from \"@livelike/javascript\"\n\ngetCommentBoardBan({\n  commentBoardBanId: '<comment_board_ban_id>',\n}).then((commentBoardBan) => console.log(commentBoardBan));",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Delete Comment Board Ban"
}
[/block]
Remove a ban by providing a ban id.

**API Definition:** [deleteCommentBoardBan](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteCommentBoardBan)
[block:code]
{
  "codes": [
    {
      "code": "import { deleteCommentBoardBan } from \"@livelike/javascript\"\n\ndeleteCommentBoardBan({\n  commentBoardBanId: '<comment_board_ban_id>',\n})",
      "language": "javascript"
    }
  ]
}
[/block]