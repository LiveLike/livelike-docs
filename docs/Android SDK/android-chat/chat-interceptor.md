---
title: Chat Interceptor
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 👍 This feature is available from 2.73.

Integrator can intercept send chat action and take decision whether to send it or not. 

```text Kotlin
chatSession.sendMessage(
    "Hello",
    null,
    null,
    object : LiveLikeCallback<LiveLikeChatMessage>() {
        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {}
    },
    chatInterceptor = { livelikeChatMessage->
    //return boolean to allow this message to send or not
    }
)
```

The Chat Stock UI also supports ChatInterceptor.\
For this integrator has to override the value chatInterceptor in ChatView.

```kotlin
chatView.chatInterceptor = object : ChatInterceptor {
                override fun invoke(p1: LiveLikeChatMessage): Boolean {
                    // return boolean
                }
            }
```
