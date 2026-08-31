---
title: react-native v0.0.1-alpha.11
author: ReadMe API
hidden: false
published_at: '2023-05-25T14:34:29.673Z'
---
### What's New:

* updated `@livelike/javascript` dependencies to `0.0.1-alpha.14` that has critical fix for `addWidgetListener` API.
* added `DismissIconComponent` prop to `LLWidgetHeader` to customise dismiss icon.

### Fixes:

* minor fix to reflect proper UI phase for mutli interaction based widgets when now UI phase transition from `SUBMITTING` to `INTERACTIVE` (instead of `SUBMITTED`).
* minor fix for `ResultBarComponent` used by result based widgets to render `View` instead of `Text` that would enable to set styles like borderRadius etc.