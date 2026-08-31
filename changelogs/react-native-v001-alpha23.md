---
title: react-native v0.0.1-alpha.23
author: ReadMe API
hidden: false
published_at: '2023-11-16T15:51:21.378Z'
---
What’s New:

* added feature to allow integrators to inject their own Analytics provider. It will have a track function which takes two parameters, Event name and track Object associated with that event. Refer [react native analytics](https://docs.livelike.com/docs/react-native-analytics) for details.
* introduced [useAnalytics](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useAnalytics) hook to enable integrators to set custom analytics provider.
* introduced [useChatMessageMenuItemAction](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useChatMessageMenuItemActions) hook. This actions returns functions which are executed when user clicks moderation menu items.
* introduced [useDebounce](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useDebounce) hook which returns a function that delays the execution of provided function until a provided time period.
* introduced [useTrackKeyboardEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useTrackKeyboardEffect) which attaches event listener to keyboard and executes `trackEvent` function when the keyboard is selected and hidden.
* introduced [useUserReactionActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useUserReactionActions) hook. This hook returns functions which are executed when user add or remove reactions.
* introduced [useWidgetInteractedAnalytics](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractedAnalytics) hook. It is used to track `Widget Interacted` analytics event.
* introduced [useWidgetSubmitAction](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetSubmitAction) hook, enabling the tracking of `Widget Submitted` analytics events and managing widget interaction submit action. It internally calls `createWidgetInteractionAction` to ensure analytics tracking is called upon successful resolution.