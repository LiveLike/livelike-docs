---
title: Analytics Event Glossary
excerpt: ''
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
[block:api-header]
{
  "title": "Widgets"
}
[/block]
Each widget analytics event has some common properties, found in the table below.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Widget ID",
    "0-1": "String",
    "0-2": "Unique identifier of the widget",
    "1-0": "Widget Type",
    "1-1": "String",
    "1-2": "Kind of widget, e.g. \"alert\", \"cheer-meter\", \"image-poll\", etc.",
    "2-0": "Program ID",
    "2-1": "String",
    "2-2": "Unique identifier of the program the widget was received on"
  },
  "cols": 3,
  "rows": 3
}
[/block]
### Widget Displayed

Fired when a user receives a widget.
[block:callout]
{
  "type": "warning",
  "body": "This is a misnomer because the SDK doesn't have control over whether a widget is actually displayed to users, that is up to your application."
}
[/block]
### Widget Became Interactive

Fired when a widget is enabled for interaction.

### Widget Interacted

Fired at every widget interaction. Includes a *Number Of Taps* property that counts the number of times a user taps on interactive elements in the widget.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Number of Taps",
    "0-1": "Number",
    "0-2": "Count of the number of taps on the widget since the previous Widget Interacted event was fired"
  },
  "cols": 3,
  "rows": 1
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "The Widget Interacted event is not fired by default when using widgets with custom user interfaces."
}
[/block]
### Widget Dismissed

Fired when a user takes an action to dismiss the widget, such as when pressing the dismiss button or swiping it away. This is event is not fired when a widget expires on its own.

### Alert Link Opened

Fired when a link on an Alert Widget is opened.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Link URL",
    "0-1": "String",
    "0-2": "URL of the link that was opened"
  },
  "cols": 3,
  "rows": 1
}
[/block]

[block:api-header]
{
  "title": "Chat Rooms"
}
[/block]
### Keyboard Selected

Fired every time the user opens the keyboard. Has a *Keyboard Type* property to represent "Sticker" or "Standard" keyboard.
[block:api-header]
{
  "title": "Chat Messages"
}
[/block]
Each analytics event related to chat messages includes the common properties below.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Chat Room ID",
    "0-1": "String",
    "0-2": "Unique identifier of the chat room the message was sent to",
    "1-0": "Chat Message ID",
    "1-1": "String",
    "1-2": "Unique identifier of the chat message"
  },
  "cols": 3,
  "rows": 2
}
[/block]
### Chat Message Sent

Fired each time user sends a message.
[block:parameters]
{
  "data": {
    "0-0": "Sticker Shortcodes",
    "0-1": "List of String",
    "0-2": "List of shortcodes of each sticker included in the message",
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description"
  },
  "cols": 3,
  "rows": 1
}
[/block]
### Chat Reaction Added

Fired each time user adds reaction to a message.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Chat Reaction ID",
    "0-1": "String",
    "0-2": "Unique identifier of the reaction added to the message"
  },
  "cols": 3,
  "rows": 1
}
[/block]
### Chat Reaction Removed

Fired each time user removes reaction from a message.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Chat Reaction ID",
    "0-1": "String",
    "0-2": "Unique identifier of the reaction removed from the message"
  },
  "cols": 3,
  "rows": 1
}
[/block]
### Chat Reaction Panel Opened

Fired each time user opens reaction panel from a message.
[block:parameters]
{
  "data": {
    "0-0": "Chat Room ID",
    "1-0": "Chat Message ID",
    "0-1": "String",
    "1-1": "String",
    "0-2": "Unique identifier of the chat room the message was sent to",
    "1-2": "Unique identifier of the chat message",
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description"
  },
  "cols": 3,
  "rows": 2
}
[/block]
### Chat Flag Action Selected

Fired when user clicks on flag to block a user/ reports a message.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Reason",
    "0-1": "String",
    "0-2": "Reason for blocking a user / reporting message"
  },
  "cols": 3,
  "rows": 1
}
[/block]
### Chat Message Link Clicked

Fired each time user clicks on a link in a chat message.
[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "Chat Room ID",
    "0-1": "String",
    "1-0": "Chat Room Title",
    "1-1": "String",
    "1-2": "Title of the Chat room used",
    "0-2": "Unique identifier of the chat room the message was sent to",
    "3-0": "Chat Message Link",
    "3-1": "String",
    "3-2": "URL of the link that was opened",
    "2-0": "Chat Message ID",
    "2-2": "Unique identifier of the chat message",
    "2-1": "String"
  },
  "cols": 3,
  "rows": 4
}
[/block]