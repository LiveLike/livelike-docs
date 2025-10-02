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

> 🚧 Web Version 2.8.0+ is required

```html
<livelike-chat roomid="" messageurls></livelike-chat>

<script>
 const livelikeChat = document.querySelector('livelike-chat');
  
 <!-- Overwrite default URL matching regex -->
 livelikeChat.messageUrlPatterns = [/custom regex/]

 <!-- Add your own regex in addition to the default provided URL matching regex -->
 const newPatterns = livelikeChat.messageUrlPatterns;
 newPatterns.push(/custom regex/);
 livelikeChat.messageUrlPatterns = newPatterns;
<script>
```

You can see the running example of how urls look in chat here:

<Embed url="https://codepen.io/tanyalivelike/pen/abwQYOP" title="Chat Message Urls" favicon="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" image="https://assets.codepen.io/6796853/internal/screenshots/pens/abwQYOP.default.png?fit=cover&amp;format=auto&amp;ha=false&amp;height=360&amp;quality=75&amp;v=2&amp;version=1632727069&amp;width=640" provider="codepen.io" href="https://codepen.io/tanyalivelike/pen/abwQYOP" html="%3Ciframe%20height%3D'350'%20scrolling%3D'no'%20src%3D'https%3A%2F%2Fcodepen.io%2Ftanyalivelike%2Fembed%2FabwQYOP'%20frameborder%3D'no'%20allowtransparency%3D'true'%20allowfullscreen%3D'true'%20style%3D'width%3A%20100%25%3B'%3E%3C%2Fiframe%3E" />
