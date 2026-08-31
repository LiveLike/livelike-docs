---
title: javascript v0.0.1-alpha.8
author: ReadMe API
hidden: false
published_at: '2023-04-11T11:50:13.455Z'
---
### What’s New:

* Added pin message API’s namely `pinMessage`, `unpinMessage` and `getPinMessageInfoList`. Refer [pin message](https://docs.livelike.com/docs/javascript-pin-messages) docs.
* Added `getTargetedWidgetIdAndKind` widget API. Refer [getTargetedWidgetIdAndKind API](https://docs.livelike.com/docs/javascript-widgets#gettargetedwidgetidandkind) doc.
* Added reward action API’s namely `getRewardActions` and `getInvokedRewardActions`. Refer [reward action](https://docs.livelike.com/docs/javascript-reward-actions) docs.
* Added quest API’s namely `getQuests`, `startUserQuest`, `getUserQuests`, `updateUserQuestTasks`, `incrementUserQuestTaskProgress`, `setUserQuestTaskProgress`, `getQuestRewards`, `getUserQuestRewards` and `claimUserQuestRewards`. Refer [quest](https://docs.livelike.com/docs/javascript-quest) docs.
* `getWidgetInteractions` also support `interactionUrl` as argument prop (similar to `getWidgetsInteractions`).
* `claimPredictionRewards` API now only supports follow up widget details (since this API needs to be used only in the case of follow up widgets).

### Fixes:

* internally refactored `getWidgetInteractions` API to extend support for follow up widgets. Internally it uses `getTargetedWidgetIdAndKind` API to get its corresponding interacted widget details and return widget interactions against that widget details. This is useful in the case of prediction followup widgets.