---
title: Web engagementsdk v2.52.0
author: ReadMe API
hidden: false
published_at: '2023-10-13T14:16:18.808Z'
---
### What’s New:

* added create widget API’s for creating, publising and deleting widget from SDK, namely `createTextPollWidget`, `createImagePollWidget`, `createTextPredictionWidget`, `createImagePredictionWidget`, `updateTextPredictionWidgetOption`, `updateImagePredictionWidgetOption`, `createPredictionFollowUpWidget`, `createTextQuizWidget`, `createImageQuizWidget`, `createAlertWidget`, `createTextAskWidget`, `publishWidget` and `deleteWidget` API. Refer [docs](https://docs.livelike.com/docs/creating-and-scheduling-widgets) for more details.
* `customId` arg prop from `createCommentBoard` API is now optional.
* added `widgetAttributes` arg prop to `getPostedWidgets` and `getWidgets` API that would enable listing widgets based on given widget attributes.