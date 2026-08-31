---
title: react-native v0.0.1-alpha.7
author: ReadMe API
hidden: false
published_at: '2023-04-11T12:05:41.343Z'
---
### What’s New:

* Added base widget components namely `LLWidget`, `LLWidgetHeader`, `LLWidgetOption`, `LLWidgetFooter` and various base child components which could be reused and customised.
* Added stand alone widget namely `LLPollWidget`, `LLQuizWidget`, `LLPredictionWidget`, `LLPredictionFollowWidget`, `LLNumberPredictionWidget`, `LLNumberPredictionFollowUpWidget` and `LLEmojiSliderWidget`. Refer [react native widgets](https://docs.livelike.com/docs/react-native-widgets) docs for further details.
* Added widget base hooks like `useWidget`, `useWidgetInteractions`, `useWidgetUIPhase`, `useLoadWidgetEffect`, `useWidgetInteractiveTimeout`, `useWidgetExpiryEffect`, `usePredictionClaimRewardEffect`, `useWidgetRewards`, `useWidgetSponsors`, `useIsWidgetDisabled`, etc. in case there’s a need to define custom presentational component but reuse our stock UI state logic.