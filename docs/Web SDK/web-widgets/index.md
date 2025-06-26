---
title: Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widgets | Web SDK | LiveLike Developer Hub
  description: >-
    This document explains LiveLike's interactive features for Web SDKs like
    polls, quizzes, and predictions that can be displayed in either popup or
    timeline mode on the web.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: web-widget-modes
      title: Widget Modes
    - type: basic
      slug: live-blog-tutorial
      title: Live Blog Tutorial
---
The various interactive elements like polls, quizzes, and predictions are called widgets. A list of the available widgets can be found in the [widgets product guide](doc:widgets).

## LiveLike Widgets

`livelike-widgets` is a native web component as part of web-sdk stock UI catalog that could be used to add LiveLike widgets into your web application. It supports different display modes to suit various use cases. This document explains the available widget modes and how to use them.

Usage example:

```html
<body>
<livelike-widgets programid="YOUR-PROGRAM-ID"></livelike-widgets>
</body>
```

Replace `YOUR-PROGRAM-ID` with your actual LiveLike Program ID

## Widget Modes

Widgets can be displayed in a variety of ways. There are two different modes supported on the web: popup and timeline. In popup mode, widgets appear one at a time, and are active for only a short while. In timeline mode, widgets don't disappear after they expire. Old widgets get pushed down, and new ones appear on top. Old ones can also be loaded from the past. [Read more about widget modes](doc:web-widget-modes) to learn how to integrate widgets on the web, and which use-cases work with which modes.