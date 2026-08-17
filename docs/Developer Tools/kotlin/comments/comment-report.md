---
title: Comment Report
excerpt: '**CommentReport** represents one report created against a comment'
deprecated: false
hidden: true
metadata:
  robots: index
---
## Create Comment Report

Users can report a comment to moderators.

**API Definition:** [createCommentReport](https://docs.livelike.com/reference/create-comment-report)

<br />

### Create A Comment Report

Use `session.reportComment()` to report a comment from the Commentboard UI flow:

```kotlin
session.reportComment(comment.id) { report, error ->
  if (error != null) {
    return@reportComment
  }

  // `report` is the newly created CommentReport.
  val reportId = report?.id
  val reportedCommentId = report?.commentId
}
```

Or use the client directly:

```kotlin
commentClient.createCommentReport(
  CreateCommentReportRequestOptions(
    commentId = comment.id
  )
) { report, error ->
  if (error != null) {
    return@createCommentReport
  }

  println("Created report: ${report?.id}")
}
```

<br />

### Comment Reports

**CommentReport** represents one report created against a comment. It is separate from **Comment**.

**Comment**

- `id` = comment ID
- `isReported` = whether the comment has been reported

**CommentReport**

- `id` = report ID
- `commentId` = comment the report belongs to
- `reportedById` = profile that created the report

Use **CommentReport** to determine whether the authenticated user can cancel a report.

| Field            | Description                                                     |
| ---------------- | --------------------------------------------------------------- |
| `id`             | The report ID. Required by `session.unReportComment(reportId)`. |
| `commentId`      | The ID of the comment being reported.                           |
| `reportedById`   | The profile ID of the user who created the report.              |
| `reportStatus`   | The report state, for example pending or dismissed.             |
| `commentBoardId` | The board containing the reported comment.                      |
| `comment`        | Optional embedded comment returned by the API.                  |

#### Important: Comment.isReported

Do not use `Comment.isReported` to decide whether to show Cancel Report.

`comment.isReported` only indicates that the comment has been reported. Multiple users can report the same comment, so it does not identify who owns a report.

To determine whether the current user owns a report, compare:

`commentReport.reportedById == currentProfileId`

### Load Reports For A Page Of Comments

After loading a page of comments, request reports for all comment IDs in one call:

```kotlin
val commentIds = comments.map { it.id }

commentClient.getCommentReports(
  GetCommentReportsRequestOptions(
    commentBoardId = commentBoardId,
    commentIds = commentIds,
    reportStatus = ReportStatusOptions.PENDING
  ),
  LiveLikePagination.FIRST
) { reports, error ->
  if (error != null) return@getCommentReports

  val myReportsByCommentId = reports.orEmpty()
    .filter { it.reportedById == currentProfileId }
    .mapNotNull { report ->
      report.commentId?.let { commentId -> commentId to report }
    }
    .toMap()

  // Use this map when rendering each comment.
}
```

The SDK sends one `comment_id` parameter for each unique ID:

```
GET /api/v1/comment-reports/
?client_id=...
&comment_board_id=...
&comment_id=comment-1
&comment_id=comment-2
&report_status=pending
```

### Show Cancel Report

```kotlin
val report = myReportsByCommentId[comment.id]

if (report != null) {
  session.unReportComment(report.id) { _, _ -> }
} else {
  session.reportComment(comment.id) { _, _ -> }
}
```

### Hide Comments Reported By The Current User

```kotlin
val visibleComments = comments.filter { comment ->
  myReportsByCommentId[comment.id] == null
}
```

For normal users, the reports API returns their own reports. Clients should still filter by `reportedById == currentProfileId`, especially for producer accounts that can manage reports created by other users.