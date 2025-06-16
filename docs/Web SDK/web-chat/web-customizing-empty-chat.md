---
title: Chat Message List States
excerpt: Customizing chat message list states such as empty and loading on the web
deprecated: false
hidden: false
metadata:
  title: Chat Message List States | Web SDK | LiveLike
  description: >-
    Customize chat message list states to mark them as empty or loading on the
    web. Learn more about Web Chat Message List States.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "warning",
  "title": "Web SDK version 1.6.3 required"
}
[/block]

[block:api-header]
{
  "title": "Empty and Loading States"
}
[/block]
Developers can provide their own templates to `<livelike-chat>` elements that will be used when those chats are loading or when they are empty.

The `<livelike-chat>` element has a couple of [slots](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/slot) that can be used to customize the look and feel of the message list depending on the state of the chat.

* The loading state, using the `message-list-loading` slot
* The empty state, using the `message-list-empty` slot

Only one of the slots will be showing at any time. When the messages are being loaded, the `message-list-loading` slot will be shown. After the messages have finished loading but there are no messages to display, the `message-list-empty` slot will be shown. Otherwise, when the messages have both loaded and is there are more than zero, the list of messages will be shown.
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/abhi1599/embed/oNwoBBv' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/abhi1599/pen/oNwoBBv",
  "title": "livelike-chat empty and loading states",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Slots are part of the Web Components spec",
  "body": "If you aren't familiar with how slots work, read more about them at [HTML <slot> element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/slot) on MDN."
}
[/block]
Here are some things to keep in mind when customizing the chat element with slots:

1. Any element can be used as a slot
2. The elements being used as slots must be direct children of the `<livelike-chat>` element
3. Elements being used as slots can have any number of children
4. Each slot name may only be used once