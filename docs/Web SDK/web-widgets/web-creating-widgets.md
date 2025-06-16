---
title: Creating Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Creating Widgets | Web SDK | Interactive Tools | LiveLike
  description: >-
    Widgets like polls, quizzes, and watch parties works to boost user
    engagement rates. Learn more about creating widgets for Web SDK.
  robots: index
next:
  description: ''
---
[block:api-header]
{}
[/block]
All of these methods can be found in the livelike-widget element [reference documentation](https://websdk.livelikecdn.com/docs/2.0.0/elements.html#livelike-widgets)

Widget can be created with multiple different methods. 

[block:callout]
{
  "type": "info",
  "title": "A widget id or widgetPayload is needed for all following methods.",
  "body": "**The following methods are for displaying widgets previously published through the API or Producer Suite.**\n\nTo handle new widgets that are being published where you do not have access to the id or payload yet, see the [Widget Modes section](doc:web-widget-modes)"
}
[/block]

[block:api-header]
{
  "title": "createWidgetElement"
}
[/block]
With `createWidgetElement`, you can immediately display a widget on the page by passing in the widget `kind` and `id`. This is useful if you just want to display a widget that has already been posted.
[block:code]
{
  "codes": [
    {
      "code": "const widgetContainer = document.querySelector('livelike-widgets');\n\nwidgetContainer.createWidgetElement({kind: 'text-poll', id: 'widgetid' });",
      "language": "javascript",
      "name": "createWidgetElement"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "showWidget"
}
[/block]
With `showWidget`, you can display a widget if you already have the `widgetPayload`. This is useful if you need to access the `widgetPayload` before displaying the widget. If you do not have the `widgetPayload` yet, the [`getWidget` method](https://websdk.livelikecdn.com/docs/2.0.0/index.html#widgets) can be used in conjunction with the `showWidget` method.
[block:code]
{
  "codes": [
    {
      "code": "const widgetContainer = document.querySelector('livelike-widgets');\n\nLiveLike.getWidget({kind: 'text-poll', id: 'widgetid' })\n  .then(widgetPayload => widgetContainer.showWidget({ widgetPayload }));",
      "language": "javascript",
      "name": "showWidget"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "createSyncWidget"
}
[/block]
The SDK has a built-in queue system by default. This is used for Spoiler Prevention when used with a custom `syncStrategy`. Learn more about [Spoiler Prevention](doc:web-spoiler-free-sync)

When creating a widget with `createSyncWidget`, it will be displayed according to the `syncStrategy`
[block:code]
{
  "codes": [
    {
      "code": "const widgetContainer = document.querySelector('livelike-widgets');\n\nwidgetContainer.createSyncWidget({kind: 'text-poll', id: 'widgetid' });",
      "language": "javascript",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "enqueueWidget"
}
[/block]
The `enqueueWidget` method works similaraly to the `showWidget` method above, except it will displayed according to the `syncStrategy`
[block:code]
{
  "codes": [
    {
      "code": "const widgetContainer = document.querySelector('livelike-widgets');\n\nLiveLike.getWidget({kind: 'text-poll', id: 'widgetid' })\n  .then(widgetPayload => widgetContainer.enqueueWidget({ widgetPayload }));",
      "language": "javascript",
      "name": "enqueueWidget"
    }
  ]
}
[/block]

[block:api-header]
{}
[/block]