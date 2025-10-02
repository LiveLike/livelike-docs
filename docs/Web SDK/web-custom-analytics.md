---
title: Web UI Analytics
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

## Implementation

The following snippet shows how you can use your own provider by passing it into the init function as `analyticsProvider`.

```javascript
LiveLike.init({ 
	clientId: "your-client-id", 
	analyticsProvider: yourAnalyticsProvider,
})
```

The `yourAnalyticsProvider` is the instance of your analytics provider. It should have a `track` function that takes two parameters - event name and event object.

See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.

## Using DOM events to implement custom analytics

If you want to integrate your own custom analytics solution, you can use the DOM events fired by the various elements provided by the Web SDK.

## Chat Analytics

Use DOM events to track the events you need. Attach listeners directly to the `<livelike-chat>` element. The list of available events include:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Event Name
      </th>

      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        messagesent
      </td>

      <td>
        When the current user sends a message
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        messagereceived
      </td>

      <td>
        When a message is received from any user
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        messagedeleted
      </td>

      <td>
        When the producer deletes a message
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        messagefailed
      </td>

      <td>
        When the request fails when sending a message
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        reactionadded
      </td>

      <td>
        When a chat reaction is added
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        reactionremoved
      </td>

      <td>
        When a chat reaction is removed
      </td>

      <td>
        \{message: Object, roomId: string}
      </td>
    </tr>

    <tr>
      <td>
        roomentered
      </td>

      <td>
        When the user loads a chat room
      </td>

      <td>
        \{ room: Element, roomId: string }
      </td>
    </tr>

    <tr>
      <td>
        roomexited
      </td>

      <td>
        When a user leaves a chat room
      </td>

      <td>
        \{ roomId: string }
      </td>
    </tr>

    <tr>
      <td>
        messagehistory
      </td>

      <td>
        When messages have been loaded
      </td>

      <td>
        \{ messages: Array\<message> }
      </td>
    </tr>
  </tbody>
</Table>

```javascript
const chatNode = document.querySelector('livelike-chat')

chatNode.addEventListener('messagesent', function (ev) {
  /* User sent a chat message! */
  myAnalytics.trackEvent('Message Sent', { messageId: ev.detail.message.id })
})
```

## Widgets Analytics

Use DOM events to track the events you need. Attach listeners directly to the `<livelike-widgets>` element. There are two kinds of events that can be tracked on the widget element. Events that relate to the creation, DOM attachment, and detachment of the actual widget itself, and events that relate to widget interactivity. The event's return two possible properties, `widget`, the object containing all the widget data, and `element`, the Element that is inserted into the DOM. The list of available widget events include:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Event name
      </th>

      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        beforewidgetattached
      </td>

      <td>
        When a widget is created but hasn't yet been attached to the DOM
      </td>

      <td>
        \{widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        widgetattached
      </td>

      <td>
        When a widget gets attached to the DOM
      </td>

      <td>
        \{element: Element, widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        beforewidgetdetached
      </td>

      <td>
        Before a widget gets detached from the DOM
      </td>

      <td>
        \{element: Element, widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        widgetdetached
      </td>

      <td>
        When a widget gets detached from the DOM
      </td>

      <td>
        \{element: Element, widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        dismiss
      </td>

      <td>
        When the user closes the widget
      </td>

      <td>
        \{element: Element, widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        expire
      </td>

      <td>
        When the widget interactivity time elapses naturally
      </td>

      <td>
        \{element: Element, widget: Object}
      </td>
    </tr>

    <tr>
      <td>
        rankchange
      </td>

      <td>
        When a user's leaderboard rank changes and receives rewards
      </td>

      <td>
        \{element: Element, widget: Object, rewards: Array}
      </td>
    </tr>
  </tbody>
</Table>

The list of available interactivity events include: 

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        vote
      </td>

      <td>
        Poll widget vote
      </td>
    </tr>

    <tr>
      <td>
        answer
      </td>

      <td>
        Quiz widget answer
      </td>
    </tr>

    <tr>
      <td>
        prediction
      </td>

      <td>
        Prediction widget answer
      </td>
    </tr>

    <tr>
      <td>
        cheer
      </td>

      <td>
        Cheer widget vote
      </td>
    </tr>

    <tr>
      <td>
        slider
      </td>

      <td>
        Slider widget vote
      </td>
    </tr>
  </tbody>
</Table>

The order in which the events are fired is as follows:

1. beforewidgetattached
2. widgetattached
3. \[ vote / answer / prediction / cheer / slider]
4. beforewidgetdetached
5. \[ dismiss / expire ]
6. widgetdetached

```javascript
const widgetsNode = document.querySelector('livelike-widgets')

widgetsNode.addEventListener('dismiss', function (ev) {
  /* A widget was explicitly dismissed by the user */
  myAnalytics.trackEvent('Widget Dismissed', { widgetId: ev.detail.widget.id })
})

['vote', 'answer', 'cheer'].forEach(function (eventName) {
  widgetsNode.addEventListener(eventName, function (ev) {
    /* A widget was interacted with */
    myAnalytics.trackEvent('Widget Interacted', { widgetId: ev.detail.widget.id })
  })
})
```