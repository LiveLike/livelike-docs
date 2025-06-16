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

> 🚧 CSS Properties are only supported in versions \< 2.0.0

> 📘 Check the reference for the full CSS documentation.
>
> Check the [CSS property reference](https://www.npmjs.com/package/@livelike/engagementsdk#theming) for all of the available CSS properties.

## Popup vs. Timeline Mode

Widgets can be styled to look differently when in [popup mode vs. timeline mode](doc:web-widget-modes). The `mode` attribute can be targeted in a CSS rule to style the two modes differently.

```css
/* Polls are now accented green in timeline mode */
livelike-widgets[mode="timeline"] {
  --theme-poll-primary-color: green;
  --theme-poll-secondary-color: green;
}
```

## Interactive vs. Disabled Widgets

Widgets in [Timeline Mode](doc:web-widget-modes) that are loaded from history are disabled. Only new ones that are published while a timeline is being displayed will be interactive. These widgets can be themed differently by targeting the `disabled` attribute in a CSS rule. This can be used to differentiate interactive widgets from disabled ones:

```css
/* Disabled quiz widgets are now accented gray */
livelike-text-quiz[disabled],
livelike-image-quiz[disabled] {
  --theme-quiz-primary-color: gray;
  --theme-quiz-secondary-color: gray;
}
```

## Hiding Borders on Past Quiz Widgets

```css
/* Past quiz widgets no longer show borders on the correct answers */
livelike-text-quiz[disabled],
livelike-image-quiz[disabled] {
  --theme-correct-border-color: transparent;
}
```
