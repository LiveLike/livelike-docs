---
title: Chat Room Switching Tutorial
excerpt: How to build a multi-room chat experience with LiveLike and Bootstrap
deprecated: false
hidden: false
metadata:
  title: Chat Room Switching Tutorial | Web SDK | LiveLike
  description: >-
    Check out this Chat Room Switching tutorial to learn how to build a multiple
    room experience that allows switching between rooms.
  robots: index
next:
  description: ''
---
In this tutorial we will use LiveLike's [chat element](doc:web-chat) and Bootstrap's [nav component with its tab behavior](https://getbootstrap.com/docs/4.4/components/navs/#javascript-behavior) to build a multiple room experience that allows switching between rooms, and only shows one room at a time.
[block:callout]
{
  "type": "info",
  "title": "Intended for LiveLike v1 and Bootstrap v4",
  "body": "This tutorial was written for LiveLike version 1.x and Bootstrap version 4.x."
}
[/block]

[block:api-header]
{
  "title": "The Idea"
}
[/block]
We will build a sidebar for the available rooms using the [nav pills component](https://getbootstrap.com/docs/4.4/components/navs/#pills) with the [.flex-column utility](https://getbootstrap.com/docs/4.4/components/navs/#vertical) to display them vertically.

We will mark up the nav and the chat elements as tabs. Marking them up that way allows us to use the [nav component JavaScript behavior](https://getbootstrap.com/docs/4.4/components/navs/#javascript-behavior) to add the interactive switching.

We want to have multiple chat elements on the page instead of having one element and then changing its `roomid` attribute. Multiple elements is preferable because changing the attribute on a single element causes a reload of the chat room and its message history which can be jarring. It is better to have a smooth switch that minimizes DOM updates, resizing, and repositioning.
[block:api-header]
{
  "title": "The Markup"
}
[/block]
The example below has 3 chat rooms controlled by 3 nav pills behaving as tabs:

* Chat Room A
* Chat Room B
* Chat Room C

Chat Room A is active by default. Pressing any of the other inactive pill tabs will switch the chat room to the associated tab panel.
[block:code]
{
  "codes": [
    {
      "code": "<div class=\"row\">\n  <div class=\"col-3\">\n    <div class=\"nav flex-column nav-pills\" id=\"chat-room-tabs\" role=\"tablist\" aria-orientation=\"vertical\">\n      <a class=\"nav-link active\" id=\"chat-room-a-tab\" data-toggle=\"pill\" href=\"#chat-room-a\" role=\"tab\" aria-controls=\"chat-room-a\" aria-selected=\"true\">Chat Room A</a>\n      <a class=\"nav-link\" id=\"chat-room-b-tab\" data-toggle=\"pill\" href=\"#chat-room-b\" role=\"tab\" aria-controls=\"chat-room-b\" aria-selected=\"false\">Chat Room B</a>\n      <a class=\"nav-link\" id=\"chat-room-c-tab\" data-toggle=\"pill\" href=\"#chat-room-c\" role=\"tab\" aria-controls=\"chat-room-c\" aria-selected=\"false\">Chat Room C</a>\n    </div>\n  </div>\n  <div class=\"col-9\">\n    <div class=\"tab-content\" id=\"chat-rooms\">\n      <div class=\"tab-pane fade show active\" id=\"chat-room-a\" role=\"tabpanel\" aria-labelledby=\"chat-room-a-tab\">\n        <livelike-chat roomid=\"example-roomid-a\"></livelike-chat>\n      </div>\n      <div class=\"tab-pane fade\" id=\"chat-room-b\" role=\"tabpanel\" aria-labelledby=\"chat-room-b-tab\">\n        <livelike-chat roomid=\"example-roomid-b\"></livelike-chat>\n      </div>\n      <div class=\"tab-pane fade\" id=\"chat-room-c\" role=\"tabpanel\" aria-labelledby=\"chat-room-c-tab\">\n        <livelike-chat roomid=\"example-roomid-c\"></livelike-chat>\n      </div>\n    </div>\n  </div>\n</div>",
      "language": "html"
    }
  ]
}
[/block]
Sample Code can be downloaded form here
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/tanyalivelike/embed/YzQqNWq' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/tanyalivelike/pen/YzQqNWq",
  "title": "Chat Room Switching Tutorial",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico"
}
[/block]