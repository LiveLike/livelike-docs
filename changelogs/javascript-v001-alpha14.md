---
title: javascript v0.0.1-alpha.14
author: ReadMe API
hidden: false
published_at: '2023-05-25T14:33:42.485Z'
---
### What's New?

* added `MULTI_INTERACTION_WIDGET_KINDS` array const that contains widget kinds which supports multiple interactions.
* deprecated `UNSUPPORTED_UPDATE_INTERACTION_WIDGET_KINDS` const, use `SINGLE_INTERACTION_WIDGET_KINDS` const instead.

### Fixes:

* fix critical issue in `addWidgetListener` API to filter out other widgetId events and invoke listener only for corresponding widgetId events.