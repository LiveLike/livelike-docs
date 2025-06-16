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
[block:callout]
{
  "type": "success",
  "body": "This feature is available from 2.73."
}
[/block]
Integrator can intercept send chat action and take decision whether to send it or not. 
[block:code]
{
  "codes": [
    {
      "code": "chatSession.sendMessage(\n    \"Hello\",\n    null,\n    null,\n    object : LiveLikeCallback<LiveLikeChatMessage>() {\n        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {}\n    },\n    chatInterceptor = { livelikeChatMessage->\n    //return boolean to allow this message to send or not\n    }\n)",
      "language": "text",
      "name": "Kotlin"
    }
  ]
}
[/block]
The Chat Stock UI also supports ChatInterceptor.
For this integrator has to override the value chatInterceptor in ChatView.
[block:code]
{
  "codes": [
    {
      "code": "chatView.chatInterceptor = object : ChatInterceptor {\n                override fun invoke(p1: LiveLikeChatMessage): Boolean {\n                    // return boolean\n                }\n            }",
      "language": "kotlin"
    }
  ]
}
[/block]