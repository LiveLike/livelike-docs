---
title: Images in Chat
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: chat-message-image-picker-web
      title: Chat Message Image Picker (Web)
    - type: basic
      slug: chat-image-picker-android
      title: Chat Message Image Picker (Android)
---
## Sending Images in Chat

Images are supported in chat messages by providing an image URL, width, and height.

```javascript
LiveLike.sendMessage({
  roomId, 
  image_url: "https://example.com/image.png",
  image_width: 50,
  image_height: 150
})
```
```swift
// Send an image message using image URL
let imageMessage = NewChatMessage(
  imageURL: URL(), 
  imageSize: CGSize(width: 100, height: 100)
)
chatSession.sendMessage(imageMessage) { result in
  switch result {
  case .success(let newMessage):
    // the message was successfully sent
  case .failure(let error):
    // handle failures
  }
}
```
```kotlin
chatSession.sendChatMessage(
    msg,
    liveLikeCallback = object : LiveLikeCallback<LiveLikeChatMessage>() {
        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {
            if (error != null) {
                Toast.makeText(this@CustomChatActivity, error, Toast.LENGTH_SHORT)
                    .show()
            } else {
                //use ChatMessage model class             
            }
        }
    })
```

The [Send a Chat Message](ref:send-chat-message) REST API endpoint is also available.

## Custom Image Picker

The stock UI for chat allows custom implementations of image pickers. For more details per platform, pease see these guides:

- [Chat Message Image Picker (Web)](doc:chat-message-image-picker-web)
- [Chat Message Image Picker (Android)](doc:chat-image-picker-android)