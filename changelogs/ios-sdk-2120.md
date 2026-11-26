---
title: iOS SDK 2.120
author: LJupcho Nastevski
hidden: false
published_at: '2026-11-26T14:45:28.437Z'
type: added
---
* excludeCommentReportThreshold query item was added to GetCommentRepliesRequestOptions.
* Integrators can now use sdk.getUserComments to get the comments that belong to the current user.
* Authentication headers can now be removed from any GET API call using the request interceptor.

<br />

Eg. usage of the request interceptor

var config = LiveLikeConfig(clientID: "YOUR_CLIENT_ID")<br />config.requestInterceptor = { request in
if request.endpoint.hasPrefix("/api/v1/comment-boards/") {
      request.removeAuthorization()
   }
}