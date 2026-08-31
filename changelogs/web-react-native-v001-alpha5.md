---
title: Web react-native v0.0.1-alpha.5
author: ReadMe API
hidden: false
published_at: '2023-02-03T09:51:27.171Z'
---
### What's new:

* introduced new hooks and refactored existing ones to let integrators easily reuse our component state.
* enable customisation of `LLGifHeader`, `LLStickerPack`, `LLBasePicker`.
* align UI components styles based on updated Stock UX design.
* introduced new component - `LLThemeSwitch`, `LLMessageListEmptyComponent`.
* improved rendering performance by moving from maintaining top level state to micro store based implementation (approach similar to nanostores).

### Fixes:

* chat message list auto scrolling issue in different scenarios for eg: when keyboard is shown or hidden.
* empty message list error in `react-native 0.71.x`
* null entries error in gif picker
* keyboard offset issue in IOS (integrators are now required to wrap `LLChat` component with `SafeAreaView` and `KeyboardAvoidingView`, refer `LLChat` docs for details)