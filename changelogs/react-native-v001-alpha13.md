---
title: react-native v0.0.1-alpha.13
author: ReadMe API
hidden: false
published_at: '2023-06-07T14:20:55.748Z'
---
### What's New?

* few disruptive changes as part of renaming component and enums.
* renamed internal used core widget container component from `LLWidget` to `LLCoreWidget` where its responsible for loading widget details and rendering widget UI
* renamed internal component `LLTimelineWidget` to more cohesive name as `LLWidget` which is used by `LLWidgets`.
* renamed `LLWidgets` component `TimelineWidgetComponent` prop name to `WidgetComponent`.
* renamed `WidgetTimelineMode` enum to `WidgetMode`.
* renamed enum value from `WidgetMode.INTERACTIVE` to `WidgetMode.INTERACTIVE_TIMELINE`.
* added `interactiveTimeout` and `onInteractiveTimeout` props to followup based widgets.

### Fixes:

* fix prediction followup UI when rendered in `LLWidgets` with popup mode.
* fix auto hiding prediction and its followup widget when interactive time is elapsed as part of `LLWidgets` in popup mode.