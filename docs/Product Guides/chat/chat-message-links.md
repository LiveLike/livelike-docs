---
title: Chat Message Links
excerpt: Controlling whether or not links are clickable in chat messages
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The stock chat message UI can be customized to automatically make links inside chat messages clickable. By the default URLs inside messages will not be made clickable, but that setting can be toggled, and the logic for recognizing URLs can be customized.

## Web SDK Integration

| Property Name          | Property Type | Description                                                                                                              |
| :--------------------- | :------------ | :----------------------------------------------------------------------------------------------------------------------- |
| enableChatMessageURLs  | Boolean       | To enable showing of clickable links to matching valid urls. By Default it is disabled.                                  |
| chatMessageUrlPatterns | String        | Comma Separated Regex Strings. These values will be used to create Regex pattern and match message text to create links. |

To enable message links add the attribute **messageurls** to the `livelike-chat` element. For comma separated url regex set `messageUrlPatterns` property of `livelike-chat` element. For Eg.

```html
<livelike-chat
        timestamps
        messagemenus
        showAvatar
        messageurls
        id="livelikeChat"
        class="livelike-chat"
      >
      </livelike-chat>
```
```css
/* below class is added to anchor links, integrators can use this class to
update the style of anchor links. For Eg. change color of link*/
    .live-like-message-anchor{
      color:red
    }
```
```javascript
  const livelikeChat = document.querySelector('livelike-chat');
  const regex = /^(http:\/\/www\.|https:\/\/www\.|http:\/\/|https:\/\/)?[a-z0-9]+([\-\.]{1}[a-z0-9]+)*\.[a-z]{2,5}(:[0-9]{1,5})?(\/.*)?$/gm;
  livelikeChat.messageUrlPatterns = [regex]
```

Current Limitations with Web SDK

1. chatMessageUrlPatterns cannot take regex strings as spaces
2. If a user post a sticker and immediately types a url link without any space then it becomes a broke message. 

## Android SDK Intergration

To show and enable links in the chat, you have to set the value of **enableChatMessageURLs** to true 

```kotlin
chat_view.enableChatMessageURLs = true
```

> 🚧 Note:
> 
> For Better performance of this feature, make sure to enable enableChatMessageURLs before setSession

To add links of your own choices like for deep linking, you can add regex to access the chat message text string as linkable or not. For that, you have to set the value of **chatMessageUrlPatterns** , it should be string.

```kotlin
chat_view.chatMessageUrlPatterns = “Validation RegEx”
```

> ❗️ Feature Availability
> 
> This feature is not available for **Flutter SDK** as of 4th Aug 2021

## iOS SDK Integration

To show and enable links in the chat messages, you have to set the value of **enableChatMessageURLs** in the Chat Session Configuration or Content Session Configuration.

The value is set to true by default and can be set to **false** to disable.

```swift Content Session
class SomeClass {
  let session: ContentSession?
	let sdk: EngagementSDK
  
   func someMethod() {
     let config = SessionConfiguration(programID: programID)
     config.chatShouldDisplayAvatar = true
     config.enableChatMessageURLs = true
     session = sdk.contentSession(config: config)
     ChatViewController().session = session
   }
}
```
```swift Chat Session
let config = ChatSessionConfig(roomId: chatRoomId)
config.enableChatMessageURLs = true
```

To add link validation of your own choice, you can add a regex to determine if the chat message text string is linkable or not. For that, you have to set the value of **chatMessageUrlPatterns**  in the Chat Session Configuration or Content Session Configuration as type String.

```swift Content Session
class SomeClass {
  let session: ContentSession?
	let sdk: EngagementSDK
  
   func someMethod() {
     let config = SessionConfiguration(programID: programID)
     config.chatShouldDisplayAvatar = true
     config.enableChatMessageURLs = true
     config.chatMessageUrlPatterns = "Validation RegEx"
     session = sdk.contentSession(config: config)
     ChatViewController().session = session
   }
}
```
```swift Chat Session
let config = ChatSessionConfig(roomId: chatRoomId)
config.enableChatMessageURLs = true
config.chatMessageUrlPatterns = "Validation RegEx"
```