---
title: Android SDK 2.52
author: Shivam Verma
hidden: false
published_at: '2022-07-04T07:01:46.377Z'
---
## What's New?

* Expose stream API for getting the error facing during the video call.
* Expose enum VideoRoomErrorType to define types of errors.
* Add a callback to the joinVideoRoom method with a default value to provide info about the successful implementation regarding initialization joining of call.
* Attach error listener stream to LiveLikeVideoView.
* Update UI for LiveLikeVideoView
* Add Error UI\
  Link: [https://docs.livelike.com/docs/android-sceenic-plugin#error-listener-stream](https://docs.livelike.com/docs/android-sceenic-plugin#error-listener-stream)
* Disable interactions on widget stock UI if current time passes interactive\_until

**Bugfix**:\
Update code for getting the default value of max character limit in chat input setting default to 150 characters.