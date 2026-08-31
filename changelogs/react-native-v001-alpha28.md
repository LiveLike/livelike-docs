---
title: react-native v0.0.1-alpha.28
author: ReadMe API
hidden: false
published_at: '2023-12-20T11:28:21.116Z'
---
### What’s new:

* introduced `useFonts` hook which would return `setFonts` function that could be used by integrators to set their custom font family. Integrators has to set corresponding font for each typeface i.e set font for regular, bold, italic, semi bold etc.
* introduced `LLText` component which is used in every component instead of `Text` to get applied custom fonts.
* introduced `useCustomFontStyle` hook which returns an evaluated styles for `Text` based Component based on fontWeight and fontStyle, these tweaked style are needed because of platform (IOS & Android) limitation for custom fonts.
* introduced `useFontFamily` hook which returns an evaluated fontFamily based on fontWeight and fontStyle.