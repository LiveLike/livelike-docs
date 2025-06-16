---
title: Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
RN SDK allows you to inject your own Analytics provider to our application. With this, you can capture crucial events and its data within the application. 

# Implementation

Your custom Analytics Provider will have a track function which takes two parameters, Event name and track Object associated with that event. You can pass it as an argument while initialising the SDK using `useInit`.

```javascript react-native
import { useInit } from '@livelike/react-native';

const sampleAnalyticsProvider = {
  track: (label, data) => {
    console.log(`Tracking "${label}" with data:`, data);
  },
};

const { profile, loaded } = useInit({
  accessToken: "xxxxxxxx"
  analyticsProvider: sampleAnalyticsProvider,
});
```

> 👍 Snack Expo playground
>
> Refer [CustomAnalytics](https://snack.expo.dev/@harshitachugh/custom-analytics-provider) snack expo playground

# List of Available Events

## Common Component Analytics

### Sticker and GIF Panels

| Event Name           | Event Object        | Description                                       |
| :------------------- | :------------------ | :------------------------------------------------ |
| Sticker Panel Opened | \{ roomId: string } | Fired each time the user opens the sticker panel. |
| Sticker Panel Closed | \{ roomId: string } | Fired each time the sticker panel is closed.      |
| GIF Panel Opened     | \{ roomId: string } | Fired each time the user opens the GIF panel.     |
| GIF Panel Closed     | \{ roomId: string } | Fired each time the GIF panel is closed.          |

### Reaction Panel

| Event Name            | Event Object                                                        | Description                                        |
| :-------------------- | :------------------------------------------------------------------ | :------------------------------------------------- |
| Reaction Panel Opened | \{ targetId: string, targetGroupId: string }                        | Fired each time the user opens the reaction panel. |
| Reaction Panel Closed | \{ targetId: string, targetGroupId: string }                        | Fired each time the reaction panel is closed.      |
| Reaction Added        | \{ targetGroupId: string, reactionId: string, reactedById: string } | Fired each time the user adds a reaction.          |
| Reaction Removed      | \{ targetGroupId: string, reactionId: string, reactedById: string } | Fired each time the user removes a reaction.       |

## Chat Analytics

| Event Name                  | Event Object                                    | Description                                           |
| :-------------------------- | :---------------------------------------------- | :---------------------------------------------------- |
| Chat Room Entered           | \{ roomId: string, room: Object }               | Fired when a chat room is loaded                      |
| Chat Message History Loaded | \{ roomId: string }                             | Fired when messages have been loaded                  |
| Chat Message Sent           | \{ roomId: string, message: Object }            | Fired when user sends a new message.                  |
| Chat Message Failed         | \{ roomId: string, error: string }              | Fired when user tries to send a message and it fails. |
| Chat Message Received       | \{ roomId: string, message: Object }            | Fired when a message is received from any user        |
| Chat Message Deleted        | \{ roomId: string, message: Object }            | Fired when user deleted a message                     |
| Chat Message Reported       | \{ messageDetails: Object, reportInfo: Object } | Fired when user reports someone's message             |
| Chat User Blocked           | \{ messageDetails: Object, blockInfo: Object }  | Fired when user blocks some other user.               |
| Chat Room Exited            | \{ roomId: string }                             | Fired when a user leaves a chat room.                 |
| Keyboard Selected           | \{ type: string }                               | Fired every time the user opens the keyboard          |
| Keyboard Hidden             | \{ type: string }                               | Fired every time when the keyboard is closed          |

## Widget Analytics

| Event Name        | Event Object                                                  | Description                                                                                                                                                                        |
| :---------------- | :------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Widget Displayed  | \{ programId: string,  widgetId: string, widgetKind: string } | Fired when a widget gets displayed.                                                                                                                                                |
| Widget Interacted | \{ widgetId: string, interactionItem: string \| Object }      | Fired at every widget interaction.                                                                                                                                                 |
| Widget Submitted  | \{ widget: Object, interactionItem: Object }                  | Fired when a widget interaction is submitted.                                                                                                                                      |
| Widget Dismissed  | \{ widgetId: string }                                         | Fired when a user takes an action to dismiss the widget, such as when pressing the dismiss button or swiping it away. This is event is not fired when a widget expires on its own. |
| Alert Link Opened | \{ url: string }                                              | Fired when a link on an Alert Widget is opened.                                                                                                                                    |
