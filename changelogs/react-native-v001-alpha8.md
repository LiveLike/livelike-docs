---
title: react-native v0.0.1-alpha.8
author: ReadMe API
hidden: false
published_at: '2023-04-28T09:32:12.433Z'
---
### What’s New:

* introduce `sliderUIComponentProps` as a new prop which could be passed to `LLEmojiSlider` component to customise Slider UI component (i.e Slider component from [react-native-slider](https://github.com/miblanchard/react-native-slider).

### Fixes:

* fix `LLQuizWidget` crash issue when submit button is pressed with no selected option.
* fix `LLWidgetHeader` text width when widget is non dismissible.
* fix submit button pressed background color.
* fix `LLChat` autoscroll issue when component is unmounted before list gets auto scrolled to bottom.
* fix `LLWidgetHeader` timer position.