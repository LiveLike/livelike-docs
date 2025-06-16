---
title: Quote Message
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Quote Messages | LiveLike Developer Hub
  description: >-
    Quoting a message allows users to quote a particular message with the user
    message. The message will be in the form of a text, image or GIF.
  robots: index
next:
  description: ''
---
Quoting a message allow the user to quote on a particular message with the user message. The message will be of the following types:

- Text
- Image/Gif

> 🚧 Custom Message
> 
> Quote Message does not support custom Messages

To enable the quote message feature in your chat

```kotlin
chatView.enableQuoteMessage = true|false
```
```html
<livelike-chat messagequotes></livelike-chat>
```
```javascript
const livelikeChatEl = document.createElement("livelike-chat")
livelikeChatEl.messagequotes = true;
```
```swift
chatViewController.messageViewController.enableQuoteMessage = true
```

## Quote Message

```kotlin
chatSession.quoteMessage(
                    message,
                    imageUrl,
                    imageWidth = 150,
                    imageHeight = 150,
                    liveLikeCallback = callback,
                    quoteMessage = currentQuoteMessage!!,
                    quoteMessageId = currentQuoteMessage!!.id!!
                )
```
```javascript
LiveLike.quoteMessage({
   roomId: "71bb626a-1f41-45e7-ad37-cfbd4d432600",
   message: "This is quoted message",
   quoteMessage: {
     id: "4532e43c-b472-44ff-8a23-d38185924462",
     created_at: "2022-03-01T12:34:13.186Z",
     message: "Test quote message",
     sender_id: "dee64ea3-fbd2-4ca1-8d89-fa097cea4ff6",
     sender_nickname: "Loyal Giraffe",
     sender_profile_url: "<sender-image-url>",
     timetoken: "16461380595171713",
     updated_at: "2022-03-01T12:34:19+0000"
   }
}).then(quotedMessage => console.log(quotedMessage))
```
```swift
session.quoteMessage(
  newMessage,
	originalMessage) { quoteMessageResult in
  	switch result {
      case .success(let quoteMessage):
      	//Success block
      case .failure(let error):
      	//Failure block
    }
}
```

## Stock UI

Quote Message is also supported by Stock UI for each platform.

**Android**:  
In order to quote a message in Android, the user can swipe right, this will allow the user to send a message over a quote message. You can also cancel the quoted message by clicking the cancel button on the quote message box over the chat input box.  
The integrator can also update the color and size of the quote message box. 

> 📘 Enable Quote Message
> 
> By Default the quoteMessage feature is disabled in ChatView.
> 
> To Enable call 
> 
> `chatView.enableQuoteMessage = true`

![](https://files.readme.io/b8afffe-Screenshot_20220301-180157_LiveLikeDemo.jpg "Screenshot_20220301-180157_LiveLikeDemo.jpg")

![](https://files.readme.io/f9b0971-Screenshot_20220301-183407_LiveLikeDemo.jpg "Screenshot_20220301-183407_LiveLikeDemo.jpg")

**Web**:  
Quote a user message in web stock UI through message menu (by clicking on three dots), this will allow the user to quote a message. You can also cancel the quoted message by clicking the cancel button on the quote message box over the chat input box.

![](https://files.readme.io/b385113-Screenshot_2022-03-01_at_7.10.23_PM.png "Screenshot 2022-03-01 at 7.10.23 PM.png")