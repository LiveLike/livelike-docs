---
title: Web Styling Cookbook
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Web Styling Cookbook | Web SDK | Web Theming | LiveLike
  description: >-
    This page covers recipes for common tasks using the custom CSS properties
    recognized by the components provided by the web SDK.
  robots: index
next:
  description: ''
---
This page covers recipes for common tasks using the custom CSS properties recognized by the components provided by the web SDK. If you want to make themes that will work across platforms, you should use the [Custom Themes](doc:custom-themes) system instead of CSS.
[block:callout]
{
  "type": "warning",
  "body": "",
  "title": "CSS Properties are only supported in versions < 2.0.0"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Check the reference for the full CSS documentation.",
  "body": "Check the [CSS property reference](https://www.npmjs.com/package/@livelike/engagementsdk#theming) for all of the available CSS properties."
}
[/block]

[block:api-header]
{
  "title": "Popup vs. Timeline Mode"
}
[/block]
Widgets can be styled to look differently when in [popup mode vs. timeline mode](doc:web-widget-modes). The `mode` attribute can be targeted in a CSS rule to style the two modes differently.
[block:code]
{
  "codes": [
    {
      "code": "/* Polls are now accented green in timeline mode */\nlivelike-widgets[mode=\"timeline\"] {\n  --theme-poll-primary-color: green;\n  --theme-poll-secondary-color: green;\n}",
      "language": "css"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Interactive vs. Disabled Widgets"
}
[/block]
Widgets in [Timeline Mode](doc:web-widget-modes) that are loaded from history are disabled. Only new ones that are published while a timeline is being displayed will be interactive. These widgets can be themed differently by targeting the `disabled` attribute in a CSS rule. This can be used to differentiate interactive widgets from disabled ones:
[block:code]
{
  "codes": [
    {
      "code": "/* Disabled quiz widgets are now accented gray */\nlivelike-text-quiz[disabled],\nlivelike-image-quiz[disabled] {\n  --theme-quiz-primary-color: gray;\n  --theme-quiz-secondary-color: gray;\n}",
      "language": "css"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hiding Borders on Past Quiz Widgets"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "/* Past quiz widgets no longer show borders on the correct answers */\nlivelike-text-quiz[disabled],\nlivelike-image-quiz[disabled] {\n  --theme-correct-border-color: transparent;\n}",
      "language": "css"
    }
  ]
}
[/block]