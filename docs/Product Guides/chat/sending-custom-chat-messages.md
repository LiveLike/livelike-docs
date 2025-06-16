---
title: Sending Custom Chat Messages
excerpt: >-
  How to integrate methods to enable users to send messages that contain custom
  data
deprecated: false
hidden: false
metadata:
  title: Sending Custom Chat Message | LiveLike Developer Hub
  description: >-
    Custom Chat enables you to send messages which could be viewed differently
    by your users. Learn more about sending custom chat messages.
  robots: index
next:
  description: ''
---
Custom Chat message enables you to send messages which could be viewed differently by your user, combined with custom view this gives you more power to create completely custom rich messages. This can be used to send rich data as a chat message that can be interpreted by integrations to perform some action or display additional content.
[block:callout]
{
  "type": "info",
  "title": "Minimum Supported SDK Version",
  "body": "iOS: 2.31\nAndroid: 2.25\nWeb: 2.11.0"
}
[/block]

[block:api-header]
{
  "title": "Sending Custom Messages"
}
[/block]
To send a custom message, you can use the `sendCustomMessage` method in the `ChatSession`. It accepts a string parameter where the integrator can send a JSON Object parsed as String.
[block:code]
{
  "codes": [
    {
      "code": "let chatSession: ChatSession\n\nchatSession.sendCustomMessage(customString) { [weak self] result in\n\t\tguard let self = self else { return }\n    switch result {\n    \tcase .failure(let error):\n      \t\t//Handle Failures\n      case .success:\n          //Custom chat message is received on the chatroom\n\t\t}\n}",
      "language": "swift"
    },
    {
      "code": "chatSession.sendCustomChatMessage(\"\\\"check1\\\": \\\"heyaa, this is for testing\\\"}\", object : LiveLikeCallback<LiveLikeChatMessage>() {\n                    override fun onResponse(result: LiveLikeChatMessage?, error: String?) {\n                        activity?.runOnUiThread {\n                            result?.let {\n                                Log.d(\"responseCode\", result.id!!)\n                            }\n                            error?.let {\n                                Toast.makeText(context, it, Toast.LENGTH_SHORT).show()\n                            }\n                        }\n                    }\n                })",
      "language": "kotlin"
    },
    {
      "code": "import LiveLike from \"@livelike/engagementsdk\";\n\nconst customData = JSON.stringify({\n  title: \"Do you like this feature\",\n  options: [\"Yes\", \"No\"]\n});\n\nLiveLike.sendCustomMessage({\n\troomId: \"6834f1fd-f24d-4538-ba51-63544f9d78eb\",\n  custom_data: customData \n});",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Custom Chat Message View"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Platform specific implementation",
  "body": "Custom chat message view implementation or customisation is different between Web, IOS and Android.\nRefer platform specific implementation to know how this could be used."
}
[/block]
Custom chat message view could be used to render your own specific view based on the `custom_data` set as per `sendCustomMessage` API  for eg: render different LiveLike widgets based on a particular type of `custom_data`. This allows user to differentiate from normal chat messages and lets you create your own informative or interactive custom chat message view.

[Web Implementation](web-custom-chat-message#web-custom-chat-message-view)
[Android Implementation](android-custom-view-in-chat)
[IOS Implementation](chat-configuration#custom-view-for-custom-data-messages)