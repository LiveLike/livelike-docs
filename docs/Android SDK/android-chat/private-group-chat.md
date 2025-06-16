---
title: Chat Rooms
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Rooms | Android SDK | LiveLike Developer Hub
  description: >-
    LiveLike's Engagement SDK allows you to create chat rooms and provide
    certain features to manage the chat rooms and its members.
  robots: index
next:
  description: ''
---
A guide for managing Chat Rooms

## Creating a Chat Room

Users can create a chat room with an optional title, optional visibility and optional list of ChatRoomTokenGate object.  
**Parameters**: Title(Optional) , Visibility(Optional,Default value: everyone), tokenGates(Optional,Default value: null)  
**Response:** ChatRoomInfo Object, it contains the newly created chatroom Id and title

```kotlin
sdk.chat().createChatRoom(
                title,
  							Visibility.everyone,
                tokenGates,
                object : LiveLikeCallback<ChatRoomInfo>() {
                    override fun onResponse(result: ChatRoomInfo?, error: String?) {
                        val response = when {
                            result != null -> "${result.title ?: "No Title"}(${result.id})"
                            else -> error
                        }
                        response?.let { it1 -> showToast(it1) }
                    }
                })
```
```java
sdk.chat().createChatRoom(
                title,
  							Visibility.everyone,
                new LiveLikeCallback<ChatRoomInfo>() {
                  	@override
                  	void onResponse(ChatRoomInfo result,String error){
                     	// if result is null then error has some value to show 
                    }
                });
```

## Update Chat Room

Users can update the chat room with title and visibility.  
**Parameters**: Title(Optional) , Visibility(Optional)  
**Response:** ChatRoomInfo Object, it contains the updated chatroom Id and title

```kotlin
sdk.chat().updateChatRoom(groupId,
                            title,
                            visibility,
                            object : LiveLikeCallback<ChatRoomInfo>() {
                                override fun onResponse(result: ChatRoomInfo?, error: String?) {
                                    
                                    error?.let {
                                        showToast(it)
                                    }
                                }
                            })
```
```java
sdk.chat().updateChatRoom(groupId,
                            title,
                            visibility,
                            new LiveLikeCallback<ChatRoomInfo>() {
                  	@override
                  	void onResponse(ChatRoomInfo result,String error){
                     	// if result is null then error has some value to show 
                    }
                });
```

<br />

## Managing Chat Room Users

See [Chat Room Membership](https://docs.livelike.com/docs/chatroom-membership-android)

## Chat Room User Mute

Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in.  
As an integrator you have the option to query our backend to find out whether a user is muted or not  inside a chat room .

```kotlin
sdk.chat().getProfileMutedStatus(<chatroom id>,
                object : LiveLikeCallback<ChatUserMuteStatus>() {
                    override fun onResponse(result: ChatUserMuteStatus?, error: String?) {
                       
                    }
                })
```

## Listening to ChatRoom Update

Whether you decide to make the user aware of their status or not, the SDK will show an alert to a muted user once they try to send a message in a room. For more information about chat moderation please see the [Chat Moderation](https://docs.livelike.com/docs/chat#moderation) page.

To subscribe to listen to updates/changes to the chatRoom, you can use the method **setChatRoomListener**, the interface **ChatRoomListener** contains the method **onChatRoomUpdate** 

```kotlin kotlin
val chatRoomListener = object : ChatRoomListener {
            override fun onChatRoomUpdate(chatRoom: ChatRoomInfo) {
                // method will auto call when new changes cames from Producer Side
            }
        }

chatsession.setChatRoomListener(chatRoomListener)
```