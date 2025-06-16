---
title: Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Analytics | Web SDK | LiveLike Developer Hub
  description: >-
    Use the DOM events fired by the various elements provided by the Web SDK to
    integrate your own custom analytics solution.
  robots: index
next:
  description: ''
---
The Engagement SDK allows you to hook into our analytic events, making it possible for you to pass through the analytics data to your own provider.
[block:api-header]
{
  "title": "Implementation"
}
[/block]
The following snippet shows how you can use your own provider by passing it into the init function as `analyticsProvider`.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.init({ \n\tclientId: \"your-client-id\", \n\tanalyticsProvider: yourAnalyticsProvider,\n})",
      "language": "javascript"
    }
  ]
}
[/block]
The `yourAnalyticsProvider` is the instance of your analytics provider. It should have a `track` function that takes two parameters - event name and event object.

See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.

[block:api-header]
{
  "title": "Using DOM events to implement custom analytics"
}
[/block]
If you want to integrate your own custom analytics solution, you can use the DOM events fired by the various elements provided by the Web SDK.
[block:api-header]
{
  "title": "Chat Analytics"
}
[/block]
Use DOM events to track the events you need. Attach listeners directly to the `<livelike-chat>` element. The list of available events include:
[block:parameters]
{
  "data": {
    "0-0": "messagesent",
    "1-0": "messagereceived",
    "0-1": "When the current user sends a message",
    "1-1": "When a message is received from any user",
    "2-0": "messagedeleted",
    "2-1": "When the producer deletes a message",
    "3-0": "messagefailed",
    "3-1": "When the request fails when sending a message",
    "4-0": "reactionadded",
    "4-1": "When a chat reaction is added",
    "5-0": "reactionremoved",
    "5-1": "When a chat reaction is removed",
    "6-0": "roomentered",
    "6-1": "When the user loads a chat room",
    "7-0": "roomexited",
    "7-1": "When a user leaves a chat room",
    "8-0": "messagehistory",
    "8-1": "When messages have been loaded",
    "h-0": "Event Name",
    "0-2": "{message: Object, roomId: string}",
    "1-2": "{message: Object, roomId: string}",
    "8-2": "{ messages: Array<message> }",
    "2-2": "{message: Object, roomId: string}",
    "6-2": "{ room: Element, roomId: string }",
    "7-2": "{ roomId: string }",
    "5-2": "{message: Object, roomId: string}",
    "4-2": "{message: Object, roomId: string}",
    "3-2": "{message: Object, roomId: string}"
  },
  "cols": 3,
  "rows": 9
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "const chatNode = document.querySelector('livelike-chat')\n\nchatNode.addEventListener('messagesent', function (ev) {\n  /* User sent a chat message! */\n  myAnalytics.trackEvent('Message Sent', { messageId: ev.detail.message.id })\n})\n",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Widgets Analytics"
}
[/block]
Use DOM events to track the events you need. Attach listeners directly to the `<livelike-widgets>` element. There are two kinds of events that can be tracked on the widget element. Events that relate to the creation, DOM attachment, and detachment of the actual widget itself, and events that relate to widget interactivity. The event's return two possible properties, `widget`, the object containing all the widget data, and `element`, the Element that is inserted into the DOM. The list of available widget events include:
[block:parameters]
{
  "data": {
    "0-0": "beforewidgetattached",
    "0-1": "When a widget is created but hasn't yet been attached to the DOM",
    "1-0": "widgetattached",
    "1-1": "When a widget gets attached to the DOM",
    "2-0": "beforewidgetdetached",
    "2-1": "Before a widget gets detached from the DOM",
    "3-0": "widgetdetached",
    "3-1": "When a widget gets detached from the DOM",
    "4-0": "dismiss",
    "4-1": "When the user closes the widget",
    "5-0": "expire",
    "5-1": "When the widget interactivity time elapses naturally",
    "0-2": "{widget: Object}",
    "1-2": "{element: Element, widget: Object}",
    "2-2": "{element: Element, widget: Object}",
    "3-2": "{element: Element, widget: Object}",
    "4-2": "{element: Element, widget: Object}",
    "5-2": "{element: Element, widget: Object}",
    "h-0": "Event name",
    "6-0": "rankchange",
    "6-1": "When a user's leaderboard rank changes and receives rewards",
    "6-2": "{element: Element, widget: Object, rewards: Array}"
  },
  "cols": 3,
  "rows": 7
}
[/block]
The list of available interactivity events include: 
[block:parameters]
{
  "data": {
    "0-0": "vote",
    "0-1": "Poll widget vote",
    "1-0": "answer",
    "1-1": "Quiz widget answer",
    "2-0": "prediction",
    "2-1": "Prediction widget answer",
    "3-0": "cheer",
    "3-1": "Cheer widget vote",
    "4-0": "slider",
    "4-1": "Slider widget vote"
  },
  "cols": 2,
  "rows": 5
}
[/block]
The order in which the events are fired is as follows:
1. beforewidgetattached
2. widgetattached
3. [ vote / answer / prediction / cheer / slider]
4. beforewidgetdetached
5. [ dismiss / expire ]
6. widgetdetached
[block:code]
{
  "codes": [
    {
      "code": "const widgetsNode = document.querySelector('livelike-widgets')\n\nwidgetsNode.addEventListener('dismiss', function (ev) {\n  /* A widget was explicitly dismissed by the user */\n  myAnalytics.trackEvent('Widget Dismissed', { widgetId: ev.detail.widget.id })\n})\n\n['vote', 'answer', 'cheer'].forEach(function (eventName) {\n  widgetsNode.addEventListener(eventName, function (ev) {\n    /* A widget was interacted with */\n    myAnalytics.trackEvent('Widget Interacted', { widgetId: ev.detail.widget.id })\n  })\n})",
      "language": "javascript"
    }
  ]
}
[/block]