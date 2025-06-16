---
title: Chat Message Urls
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Message URLs | Web SDK | LiveLike
  description: >-
    Chat message URL linking can be enabled by adding to 'messageurls' property
    to the livelike-chat element. Learn more.
  robots: index
next:
  description: ''
---
Chat message URL linking can be enabled by adding to `messageurls` property to the livelike-chat element.

The chat message url linking works through regex matching. The default regex can be found in the livelike-chat element's `messageUrlPatterns` property.

Overwriting or adding your own custom regex to the messageUrlPatterns property is possible by setting the property directly. 
[block:callout]
{
  "type": "warning",
  "title": "Web Version 2.8.0+ is required"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<livelike-chat roomid=\"\" messageurls></livelike-chat>\n\n<script>\n const livelikeChat = document.querySelector('livelike-chat');\n  \n <!-- Overwrite default URL matching regex -->\n livelikeChat.messageUrlPatterns = [/custom regex/]\n\n <!-- Add your own regex in addition to the default provided URL matching regex -->\n const newPatterns = livelikeChat.messageUrlPatterns;\n newPatterns.push(/custom regex/);\n livelikeChat.messageUrlPatterns = newPatterns;\n<script>",
      "language": "html"
    }
  ]
}
[/block]
You can see the running example of how urls look in chat here:
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/tanyalivelike/embed/abwQYOP' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/tanyalivelike/pen/abwQYOP",
  "title": "Chat Message Urls",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico",
  "image": "https://assets.codepen.io/6796853/internal/screenshots/pens/abwQYOP.default.png?fit=cover&amp;format=auto&amp;ha=false&amp;height=360&amp;quality=75&amp;v=2&amp;version=1632727069&amp;width=640"
}
[/block]