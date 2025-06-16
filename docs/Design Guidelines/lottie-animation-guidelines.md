---
title: Lottie Animation Guidelines
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Lottie Animation Guidelines | Design Guidelines | LiveLike
  description: >-
    The iOS and Android SDKs come with built-in win/lose animations for widget
    interactions. Learn more.
  robots: index
next:
  description: ''
---
The iOS and Android SDKs come with built-in win/lose animations for widget interactions. These animations can be overridden as explained in the [iOS](ios-overriding-default-lottie-animations) and [Android](https://docs.livelike.com/docs/android-customization#section-animation-overrides) docs respectively. The following guidelines explain how the design assets can be created:
[block:api-header]
{
  "title": "Guidelines"
}
[/block]
The following guidelines can be used to create LiveLike widget animations:

1. Follow the instruction to download and install the Lottie plug-in ["Bodymovin" in After Effects](https://airbnb.io/lottie/#/after-effects). We **recommend version 5.3.4** since we have noticed rare issues with exports from newer versions.
2. After installing, create a composition.
    a. Sizes are listed below, standard is 300*200
    b. Animations should not include text, only images. You can do this by right clicking “Text Element” > “Create” > “Create Shapes From Text”.
3. Follow the [Lottie instructions](https://airbnb.io/lottie/#/after-effects?id=creating-lottie-animations) to make animation. 
4. Export the composition as JSON file.
5. You can [preview your Lottie animation](https://airbnb.io/lottie/#/after-effects?id=_10-download-lottie-files-preview-app) in the mobile app before using it.
[block:api-header]
{
  "title": "Animations List"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Function",
    "h-1": "Dimensions",
    "h-2": "Duration",
    "0-0": "Standard Win (Quiz, Prediction, Cheer Meter)",
    "1-0": "Standard Lose (Quiz, Prediction, Cheer Meter)",
    "0-1": "300 x 200",
    "1-1": "300 x 200",
    "0-2": "3 seconds",
    "1-2": "3 seconds"
  },
  "cols": 3,
  "rows": 2
}
[/block]