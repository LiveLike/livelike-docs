---
title: Web engagementsdk v2.50.0
author: ReadMe API
hidden: false
published_at: '2023-09-05T11:45:39.549Z'
---
### What New:

* added `excludeDeletedCommentWithNoReplies` argument properties to `getComments` and `getCommentReplies` API’s.
* replaced `created_by` with `created_by_id` in comment board model.

### Fixes:

* added a fix for `livelike-comments` component to properly show comment/reply count when comment or reply list has deleted comments or filtered comments.