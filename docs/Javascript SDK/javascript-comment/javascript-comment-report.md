---
title: Comment Report
excerpt: >-
  A resource that represents a report submitted for comment. Users can report
  offensive comments to moderators.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Create Comment Report

Users can report a comment to moderators.

**API Definition:** [createCommentReport](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createCommentReport)

```javascript
import { createCommentReport } from "@livelike/javascript"

createCommentReport({
  commentId: '<comment_id>',
  description: '<Reason for reporting>',
}).then((commentReport) => console.log(commentReport));
```



## Get Comment Report List

Get a list of comment reports i.e. the reports submitted for comment in the current application. Each comment report resource represents information about a report submitted for comment.

**API Definition:** [getCommentReports](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentReports)

```javascript
import { getCommentReports, CommentReportStatus } from "@livelike/javascript"

getCommentReports({
  commentBoardId: '<comment_board_id>',
  commentId: '<comment_id>',
  reportStatus: CommentReportStatus.PENDING,
}).then((paginatedResponse) => console.log(paginatedResponse));
```



## Get Comment Report

Get a report submitted for a comment.

**API Definition:** [getCommentReport](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getCommentReport)

```javascript
import { getCommentReport } from "@livelike/javascript"

getCommentReport({
  commentReportId: '<comment_report_id>',
}).then((commentReport) => console.log(commentReport));
```



## Delete Comment Report

Delete a comment report resource.

**API Definition:** [deleteCommentReport](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteCommentReport)

```javascript
import { deleteCommentReport } from "@livelike/javascript"

deleteCommentReport({
  commentReportId: '<comment_report_id>',
})
```



## Dismiss a Comment Report

Dismiss a comment report. This updates the `report_status` to 'dismissed'.

**API Definition:** [dismissCommentReport](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=dismissCommentReport)

```javascript
import { dismissCommentReport } from "@livelike/javascript"

dismissCommentReport({
  commentReportId: '<comment_report_id>',
}).then((commentReport) => console.log(commentReport));
```



## Dismiss All Comment Reports

Dismiss all the reports associated with a specific comment. This updates the `report_status` of all such reports to 'dismissed'.

**API Definition:** [dismissAllCommentReports](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=dismissAllCommentReports)

```javascript
import { dismissAllCommentReports } from "@livelike/javascript"

dismissAllCommentReports({
  commentBoardId: '<comment_board_id>',
  commentId: '<comment_id>',
})
```