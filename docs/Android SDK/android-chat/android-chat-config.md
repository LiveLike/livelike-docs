---
title: Chat Configuration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Configuration | Android SDK | LiveLike
  description: >-
    Learn more about Android SDK Chat Configuration including updating chat
    nicknames, updating user avatars, and more.
  robots: index
next:
  description: ''
---
## Update Chat Nickname

When you initialize Chat the user will have a default nickname. If you want to customize it to match your application's username or provide a way to manually set it, you can use the following method.

```kotlin Kotlin
sdk.profile().updateChatNickname(nickname)
```

## Update User Avatar

You can update the user avatar at the chat room level.  
We have a default image for an avatar for placeholder and error. To set your own default image just add an image in drawable named "default_avatar.png" to override the SDK default avatar image

```kotlin Kotlin
chatsession.avatarUrl="<url>"
```
```java
chatsession.setAvatarUrl("<url>")
```

## Chat Avatar Toggle

You can toggle the showing of the user avatar at the chat room level.

```kotlin
chatView.shouldDisplayAvatar= <true|false>
```
```java
chatsession.setShouldDisplayAvatar(<true|false>)
```

## Chat Input Visibility

In a scenario where you wish to create what is called Influencer Chat, you as an integrator have the ability to create a chat experience where a user does not have an option to send any messages only view the incoming ones.

```kotlin
chat_view.isChatInputVisible = true // Hides the chat input
```

## Show Url as HyperLink in ChatView

In a scenario where you wish to show URL as a hyperlink in ChatView.

```kotlin
chatView.enableChatMessageURLs = true
```

## Configure the Sticker Keyboard

To add or remove Stickers from the keyboard, you will need to share sticker packs with LiveLike. See [Chat Sticker Guidelines](https://docs.livelike.com/docs/chat-sticker-guidelines) for more details.

## Get Unread Message Count Between Sessions

To count unread messages between app sessions you need to keep track of the timestamp of the first unread message received on each channel. With this timestamp you will call the Join API with parameter startTimeStamp to resume the stream of messages from the last timestamp or can use in combination of _Count API_

1. Maintain a dictionary of the timestamps of the first unread message of each room id
   1. Add to dict when a new message has been received on a channel that is not being displayed
   2. Remove from dict at roomID when you’ve entered the room at roomID
2. Save data to persistent storage to restore after the app closes or goes to background. 

```kotlin
chatSession.joinChatRoom("<custom-room-id>", < unix startTimestamp>)
privateGroupChatsession?.setMessageListener(object : MessageListener {
                override fun onNewMessage(chatRoom: String, message: LiveLikeChatMessage) {
                    chatRoomLastTimeStampMap[chatRoom] = Calendar.getInstance().timeInMillis
                    if (chatRoom == privateGroupChatsession?.getActiveChatRoom?.invoke()) {
                        messageCount[chatRoom] = mutableSetOf() // reset unread message count
                        chatRoomLastTimeStampMap[chatRoom] = Calendar.getInstance().timeInMillis
                    } else {
                        if (messageCount[chatRoom] == null) {
                            messageCount[chatRoom] = mutableSetOf(message.id.toString())
                        } else {
                            messageCount[chatRoom]?.add(message.id.toString())
                        }
                    }
                    getSharedPreferences("test-app", Context.MODE_PRIVATE).edit().putString("unread_count", GsonBuilder().create().toJson(messageCount)).apply(
                }
            })
```
```java
chatSession.joinChatRoom("<custom-room-id>");
        chatSession.setMessageListener(
                new MessageListener() {
                    @Override
                    public void onNewMessage(@NotNull String chatRoom, @NotNull LiveLikeChatMessage message) {
                        chatRoomLastTimeStampMap[chatRoom] = Calendar.getInstance().timeInMillis
                        if (chatRoom == chatSession.getActiveChatRoom.invoke()) {
                            messageCount[chatRoom] = mutableSetOf() // reset unread message count
                            chatRoomLastTimeStampMap[chatRoom] = Calendar.getInstance().timeInMillis
                        } else {
                            if (messageCount[chatRoom] == null) {
                                messageCount[chatRoom] = mutableSetOf(message.id.toString())
                            } else {
                                messageCount[chatRoom] ?.add(message.id.toString())
                            }
                        }
                        getSharedPreferences("test-app", Context.MODE_PRIVATE).edit().putString("unread_count", GsonBuilder().create().toJson(messageCount)).apply(
                    }
                });
```

## Custom chat room inside a session

If the integrator doesn’t want to show the public chat. In order to achieve this, they should set the custom chat room before setting it to the chat_view.

```kotlin
val chatSession = engagementSDK.createContentSession("<chat-program-id>")
chatSession.enterChatRoom("<custom-room-id>")

chatSession.joinChatRoom("<custom-room-id>", @optional startTimestamp)
```
```java
LiveLikeChatSession chatSession = engagementSDK.createChatSession("<chat-program-id>");
        chatSession.enterChatRoom("<custom-room-id>");

        chatSession.joinChatRoom("<custom-room-id>", @optional startTimestamp);
```

startTimestamp is optional-field, it can be used to replay history to handle various use cases like calculating count between session

## Chat: Message Timestamp Display

Override Default formatter

```kotlin
class ChatViewWrapper(context: Context, private val attrs: AttributeSet?) : ChatView(context, attrs) {
   override fun formatMessageDateTime(messageUnixTimeStamp: Long): String {
        return customFormatter.fromat(messageUnixTimeStamp)
    }
}
```
```java
class ChatViewWrapper extends ChatView{

        public ChatViewWrapper(@NotNull Context context, @Nullable AttributeSet attrs) {
            super(context, attrs);
        }

        @NotNull
        @Override
        public String formatMessageDateTime(@Nullable Long messageTimeStamp) {
            return customFormatter.formatMessageDateTime(messageTimeStamp);
        }
    }
```

## External Keyboard Support

Users can add image/emoji/gif coming from from any custom keyboard (Bijmoji, Giphy, Google Keyboard, etc. )

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/13167cf-Image_2020-03-20_at_8.59.15_AM.png",
        "Image 2020-03-20 at 8.59.15 AM.png",
        718
      ],
      "align": "center",
      "caption": "Gboard in action"
    }
  ]
}
[/block]


As an integrator you have the control about activating or deactivating this feature  

```kotlin
As soon as your chat view is instantiated you can call the following

// Enable the External Keyboard Support
chat_view.allowMediaFromKeyboard = true

// Disable the External Keyboard Support
chat_view.allowMediaFromKeyboard = false
```
```java
As soon as your chat view is instantiated you can call the following

// Enable the External Keyboard Support
chat_view.allowMediaFromKeyboard = true;

// Disable the External Keyboard Support
chat_view.allowMediaFromKeyboard = false;
```

## Hide Reaction Panel

To hide the reaction panel in the chat view,integrator can call the below method

```kotlin
chat_view.hidePopUpReactionPanel()
```