---
title: Widget Anatomy
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: react-native-widget-ui-lifecycle
      title: Widget UI Lifecycle
---
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8751d31-Group_64.svg",
        null,
        "Widget Anatomy"
      ],
      "align": "center",
      "caption": "Widget Anatomy"
    }
  ]
}
[/block]

Every widget follows similar UI structure where its mostly composed with Header, Body and Footer component. Every widget is capable enough to either extend default component with your own custom tweaks or render your own custom component in place of these default rendered sub component.   

## Header Component

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7baefa3-Group_68_1.svg",
        null,
        "Header Component"
      ],
      "align": "center",
      "sizing": "600px"
    }
  ]
}
[/block]

Every widget header component is defaulted to [LLWidgetHeader](react-native-llwidgetheader). It is responsible for rendering:

- Timer component (defaulted to [LLWidgetInteractiveTimer](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetInteractiveTimer)) incase widget is interact-able for certain time period only.
- Title of the widget.
- Dismiss button incase widget is dismissible.

## Body Component

Body component forms the core UI of a widget and that's the reason it is different for every widget where you could still extend default corresponding widget body component to quickly customise widget core UI. For example:

1. Poll & Prediction based widget: It renders selectable poll options and poll results.
2. Quiz based widget: It renders selectable quiz choices, results and vote numbers.
3. Number Prediction based widget: It renders options, number inputs and vote results.
4. Slider based widget: It renders slider UI
5. Cheer meter widget: It renders pressable options

For more details on the body component, refer corresponding widget `BodyComponent` prop documentation for more details.

## Footer Component

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6d31b37-Group_69.svg",
        null,
        "Footer component"
      ],
      "align": "center",
      "sizing": "750px",
      "caption": "Footer component"
    }
  ]
}
[/block]

Every widget footer is defaulted to [LLWidgetFooter](react-native-llwidgetfooter). It is responsible for rendering:

1. Submit button in case widget is one time interact-able for example quiz, emoji slider, number prediction etc.
2. Widget Rewards
3. Widget End phase Label in case widget interactivity is timed out or widget gets expired.
4. Widget sponsors.