---
title: Analytics Event Glossary
deprecated: false
hidden: false
metadata:
  title: Analytics Event Glossary | LiveLike Developer Hub
  description: >-
    Each widget analytics event has common properties in terms of type, ID, and
    more. Learn more about widget analytics.
  robots: index
next:
  description: ''
---
These are the analytics events that are triggered by the stock SDK UIs.

## Widgets

Each widget analytics event has some common properties, found in the table below.

| Property    | Type   | Description                                                     |
| :---------- | :----- | :-------------------------------------------------------------- |
| Widget ID   | String | Unique identifier of the widget                                 |
| Widget Type | String | Kind of widget, e.g. "alert", "cheer-meter", "image-poll", etc. |
| Program ID  | String | Unique identifier of the program the widget was received on     |

### Widget Events

| Event Name          | Description                                                                                                                                                                                  |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `widget_displayed`  | Fired when a widget becomes visible in a user's viewport. Maps to the **Impressions** metric. Widgets may be displayed without any interaction, this event counts exposure.                  |
| `widget_interacted` | Fired when a user submits a response on any widget type (poll vote, prediction answer, quiz answer, cheer tap, etc.). Maps to the **Interactions** metric and drives **Engagement Percent**. |
| `widget_dismissed`  | Fired when a user explicitly closes or dismisses a widget without submitting a response. Useful for diagnosing widgets that are visible but not compelling enough to drive interaction.      |

<br />

## Chat Rooms

### Keyboard Selected

Fired every time the user opens the keyboard. Has a _Keyboard Type_ property to represent "Sticker" or "Standard" keyboard.

## Chat Messages

Each analytics event related to chat messages includes the common properties below.

| Property        | Type   | Description                                                |
| :-------------- | :----- | :--------------------------------------------------------- |
| Chat Room ID    | String | Unique identifier of the chat room the message was sent to |
| Chat Message ID | String | Unique identifier of the chat message                      |

### Chat Message Sent

Fired each time user sends a message.

| Property           | Type           | Description                                                |
| :----------------- | :------------- | :--------------------------------------------------------- |
| Sticker Shortcodes | List of String | List of shortcodes of each sticker included in the message |

### Chat Reaction Added

Fired each time user adds reaction to a message.

| Property         | Type   | Description                                            |
| :--------------- | :----- | :----------------------------------------------------- |
| Chat Reaction ID | String | Unique identifier of the reaction added to the message |

### Chat Reaction Removed

Fired each time user removes reaction from a message.

| Property         | Type   | Description                                                |
| :--------------- | :----- | :--------------------------------------------------------- |
| Chat Reaction ID | String | Unique identifier of the reaction removed from the message |

### Chat Reaction Panel Opened

Fired each time user opens reaction panel from a message.

| Property        | Type   | Description                                                |
| :-------------- | :----- | :--------------------------------------------------------- |
| Chat Room ID    | String | Unique identifier of the chat room the message was sent to |
| Chat Message ID | String | Unique identifier of the chat message                      |

### Chat Flag Action Selected

Fired when user clicks on flag to block a user/ reports a message.

| Property | Type   | Description                                    |
| :------- | :----- | :--------------------------------------------- |
| Reason   | String | Reason for blocking a user / reporting message |

### Chat Message Link Clicked

Fired each time user clicks on a link in a chat message.

| Property          | Type   | Description                                                |
| :---------------- | :----- | :--------------------------------------------------------- |
| Chat Room ID      | String | Unique identifier of the chat room the message was sent to |
| Chat Room Title   | String | Title of the Chat room used                                |
| Chat Message ID   | String | Unique identifier of the chat message                      |
| Chat Message Link | String | URL of the link that was opened                            |