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

> 📘 Minimum Supported SDK Version
>
> iOS: 2.31\
> Android: 2.25\
> Web: 2.11.0

## Sending Custom Messages

To send a custom message, you can use the `sendCustomMessage` method in the `ChatSession`. It accepts a string parameter where the integrator can send a JSON Object parsed as String.

```swift
let chatSession: ChatSession

chatSession.sendCustomMessage(customString) { [weak self] result in
		guard let self = self else { return }
    switch result {
    	case .failure(let error):
      		//Handle Failures
      case .success:
          //Custom chat message is received on the chatroom
		}
}
```
```kotlin
chatSession.sendCustomChatMessage("\"check1\": \"heyaa, this is for testing\"}", object : LiveLikeCallback<LiveLikeChatMessage>() {
                    override fun onResponse(result: LiveLikeChatMessage?, error: String?) {
                        activity?.runOnUiThread {
                            result?.let {
                                Log.d("responseCode", result.id!!)
                            }
                            error?.let {
                                Toast.makeText(context, it, Toast.LENGTH_SHORT).show()
                            }
                        }
                    }
                })
```
```javascript
import LiveLike from "@livelike/engagementsdk";

const customData = JSON.stringify({
  title: "Do you like this feature",
  options: ["Yes", "No"]
});

LiveLike.sendCustomMessage({
	roomId: "6834f1fd-f24d-4538-ba51-63544f9d78eb",
  custom_data: customData 
});
```

## Custom Chat Message View

> 📘 Platform specific implementation
>
> Custom chat message view implementation or customisation is different between Web, IOS and Android.\
> Refer platform specific implementation to know how this could be used.

Custom chat message view could be used to render your own specific view based on the `custom_data` set as per `sendCustomMessage` API  for eg: render different LiveLike widgets based on a particular type of `custom_data`. This allows user to differentiate from normal chat messages and lets you create your own informative or interactive custom chat message view.

[Web Implementation](web-custom-chat-message#web-custom-chat-message-view)\
[Android Implementation](android-custom-view-in-chat)\
[IOS Implementation](chat-configuration#custom-view-for-custom-data-messages)
