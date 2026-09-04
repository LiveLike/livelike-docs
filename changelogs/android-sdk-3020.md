---
title: Android SDK 3.0.20
author: Viktor Manev
hidden: false
published_at: '2026-09-04T13:24:43.257Z'
type: fixed
---
## Comments

<br />

- Fixed duplicate query parameters when paginating with `getComments(), getCommentsPage(), `and `getCommentReplies().`
- `CommentSession.loadNextHistory()` also benefits from this fix because it uses these comment APIs internally.
- Filters such as `comment_board_id`, `ordering`, `top_level`  are no longer appended repeatedly on next/previous page requests.
- When request parameters change, pagination resets to the first page for the new query.

<br />

<br />