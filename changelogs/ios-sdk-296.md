---
title: iOS SDK 2.96
author: jelzon monzon
hidden: false
published_at: '2024-10-15T21:00:22.318Z'
---
# What's New?

* [Analytics] - Adds `Widget Prompt` attribute to `Widget Engaged` and `Widget Interacted` events. The value with be either the widget's question or title; if either exist.

# Bugfixes

* [Localization] Fixed an issue where overriding localized text from a `Localized.strings` in `main` bundle was not working.
* [Comments] Fixed an issue where getting `next` pages of `getCommentsPage` requests would not return expected page.
* [Widgets] Fixed an issue where overriding `LottieFilepaths` with empty values does not disable Lottie animations as expected.