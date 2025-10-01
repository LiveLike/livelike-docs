---
title: SDK Analytics Event Glossary
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
## Widgets

Each widget analytics event has some common properties, found in the table below.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Property
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Widget ID
      </td>

      <td style={{ textAlign: "left" }}>
        String
      </td>

      <td style={{ textAlign: "left" }}>
        Unique identifier of the widget
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Widget Type
      </td>

      <td style={{ textAlign: "left" }}>
        String
      </td>

      <td style={{ textAlign: "left" }}>
        Kind of widget, e.g. "alert", "cheer-meter", "image-poll", etc.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Program ID
      </td>

      <td style={{ textAlign: "left" }}>
        String
      </td>

      <td style={{ textAlign: "left" }}>
        Unique identifier of the program the widget was received on
      </td>
    </tr>
  </tbody>
</Table>

### Widget Displayed

Fired when a user receives a widget.

> 🚧 This is a misnomer because the SDK doesn't have control over whether a widget is actually displayed to users, that is up to your application.

### Widget Became Interactive

Fired when a widget is enabled for interaction.

### Widget Interacted

Fired at every widget interaction. Includes a *Number Of Taps* property that counts the number of times a user taps on interactive elements in the widget.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Number of Taps
      </td>

      <td>
        Number
      </td>

      <td>
        Count of the number of taps on the widget since the previous Widget Interacted event was fired
      </td>
    </tr>
  </tbody>
</Table>

> 🚧 The Widget Interacted event is not fired by default when using widgets with custom user interfaces.

### Widget Dismissed

Fired when a user takes an action to dismiss the widget, such as when pressing the dismiss button or swiping it away. This is event is not fired when a widget expires on its own.

### Alert Link Opened

Fired when a link on an Alert Widget is opened.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Link URL
      </td>

      <td>
        String
      </td>

      <td>
        URL of the link that was opened
      </td>
    </tr>
  </tbody>
</Table>

## Chat Rooms

### Keyboard Selected

Fired every time the user opens the keyboard. Has a *Keyboard Type* property to represent "Sticker" or "Standard" keyboard.

## Chat Messages

Each analytics event related to chat messages includes the common properties below.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Chat Room ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat room the message was sent to
      </td>
    </tr>

    <tr>
      <td>
        Chat Message ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Message Sent

Fired each time user sends a message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Sticker Shortcodes
      </td>

      <td>
        List of String
      </td>

      <td>
        List of shortcodes of each sticker included in the message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Reaction Added

Fired each time user adds reaction to a message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Chat Reaction ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the reaction added to the message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Reaction Removed

Fired each time user removes reaction from a message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Chat Reaction ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the reaction removed from the message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Reaction Panel Opened

Fired each time user opens reaction panel from a message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Chat Room ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat room the message was sent to
      </td>
    </tr>

    <tr>
      <td>
        Chat Message ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Flag Action Selected

Fired when user clicks on flag to block a user/ reports a message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Reason
      </td>

      <td>
        String
      </td>

      <td>
        Reason for blocking a user / reporting message
      </td>
    </tr>
  </tbody>
</Table>

### Chat Message Link Clicked

Fired each time user clicks on a link in a chat message.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Chat Room ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat room the message was sent to
      </td>
    </tr>

    <tr>
      <td>
        Chat Room Title
      </td>

      <td>
        String
      </td>

      <td>
        Title of the Chat room used
      </td>
    </tr>

    <tr>
      <td>
        Chat Message ID
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the chat message
      </td>
    </tr>

    <tr>
      <td>
        Chat Message Link
      </td>

      <td>
        String
      </td>

      <td>
        URL of the link that was opened
      </td>
    </tr>
  </tbody>
</Table>