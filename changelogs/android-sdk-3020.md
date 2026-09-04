---
title: Android SDK 3.0.20
author: Viktor Manev
hidden: true
published_at: '2026-09-04T13:24:43.257Z'
type: fixed
---
<br />

## Comments

- Fixed duplicate query parameters when loading additional comment pages.
- `getComments()`, `getCommentsPage()`, comment replies, and `CommentSession.loadNextHistory()` now use the API-provided pagination URL directly.
- Filters such as `comment_board_id`, `ordering`, `top_level`, and `without_deleted_thread` are no longer appended repeatedly on next/previous page requests.
- When request parameters change, pagination resets to the first page for the new query.

<br />

<br />