---
title: ChatRoom Membership (Android)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Chat Room Membership is a simple concept of a relationship between a user and a chat room. Once a profile joins a room, they are a member of that room until they leave it.With the functions mentioned below you will have the ability to build out a fully fleshed out chat experience. You will be able to create, delete chat room memberships, in addition you be able to retrieve all rooms a user is a member of and get all memberships in a room.

<br />

## Get chatroom memberships for the current user

<br />

In order to retrieve all the chat rooms a user is currently a member of, use getCurrentUserChatRoomList function\
**Parameters:** LiveLikePagination(enum) FIRST(default),PREVIOUS,NEXT\
**Response:** List of ChatRoomInfo(chatRoom id ,title)

```kotlin
sdk.chat().getCurrentUserChatRoomList(
                LiveLikePagination.FIRST,
                object : LiveLikeCallback<List<ChatRoomInfo>>() {
                    override fun onResponse(result: List<ChatRoomInfo>?, error: String?) {
                        
                        result?.let { it1 ->
                            chatRoomList.addAll(it1)
                        }
                        error?.let {
                            showToast(it)
                        }
                    }
                })
```
```java
sdk.chat().getCurrentUserChatRoomList(
                LiveLikePagination.FIRST,
                new LiveLikeCallback<List<ChatRoomInfo>>() {
                   @override 
                     void onResponse(List<ChatRoomInfo> result,String error) {
                       
                    }
                });
```

<br />

## Get chatroom memberships for a given chat room

<br />

User can retrieve all chat room memberships for a specific chat room\
**Parameter**: chatRoom Id  and LiveLikePagination(enum) FIRST(default),PREVIOUS,NEXT\
**Response:** List of User(LiveLikeUser)

```kotlin
sdk.chat().getMembersOfChatRoom(id,
                    LiveLikePagination.FIRST,
                    object : LiveLikeCallback<List<LiveLikeUser>>() {
                        override fun onResponse(result: List<LiveLikeUser>?, error: String?) {
                            result?.let { list ->
                                if (list.isNotEmpty()) {
                                    AlertDialog.Builder(this@ChatOnlyActivity).apply {
                                        setTitle("Room Members")
                                        setItems(list.map { it.nickname }
                                            .toTypedArray()) { _, which ->
                                            // On change of theme we need to create the session in order to pass new attribute of theme to widgets and chat
                                        }
                                        create()
                                    }.show()
                                }
                            }
                        }
                    })

//from SDK 2.81 onwards, supports filter of multiple profile ids
sdk.chat().getChatRoomMemberships(
                        ChatRoomRequestOptions(
                            chatRoomId = id,
                            profileIds = listOf(
                                "d40aca8a-d11d-4a1f-a036-b1dc0e6454e9",
                                "143571b2-5a30-4ba8-b956-6b5b73f85e69"
                            ),
                            liveLikePagination = LiveLikePagination.FIRST
                        )
                    ) { result, error ->
                        result?.let {
                            //get list of livelike profile
                        }
                    }
```
```java
sdk.chat().getMembersOfChatRoom(id,
                    LiveLikePagination.FIRST,
                    new LiveLikeCallback<List<LiveLikeUser>>() {
                        @override 
                          void onResponse(List<LiveLikeUser> result,String error) {

                                }
                            }
                        }
                    });
```

<br />

## Get common chatroom between multiple users

This provides list of chat room memberships that reflects common chatroom between the provided profileIds

```kotlin
// This gives memberships for a chat rooms
// where profile-id-1, profile-id-2 and profile-id-3 are already a member
// useful for finding common chat room between list of users
sdk.chat().getProfileChatRoomMemberships(
                        ProfileChatRoomMembershipRequestOption(
                            profileIds = listOf(
                                "<profile-id-1>",
                                "<profile-id-2>",
                                "<profile-id-3>",
                            ), liveLikePagination = LiveLikePagination.FIRST
                        )
                    ) { result, error ->
                        result?.let {
                           // list of chat room membership
                        }
                    }
```

<br />

## Join a Chat Room

User can join the chat room by providing the chatroom Id\
**Parameters:** chatRoom id\
**Response:**  ChatRoomMembership object which contains the membership id and user details

```kotlin
sdk.chat().addCurrentUserToChatRoom(id,
                object : LiveLikeCallback<ChatRoomMembership>() {
                    override fun onResponse(result: ChatRoomMembership?, error: String?) {
                        result?.let {
                            showToast("User Added Successfully")
                        }
                        error?.let {
                            showToast(it)
                        }
                    }
                })
```
```java
sdk.chat().addCurrentUserToChatRoom(id,
                 new LiveLikeCallback<ChatRoomMembership>() {
                  	@override
                  	void onResponse(ChatRoomMembership result,String error){
                     	// if result is null then error has some value to show 
                    }
                });
```

<br />

## Leave Chat Room

User can leave the group by providing the chatroom Id\
**Parameters:** chatRoom id\
**Response:**  Boolean response

```kotlin
sdk.chat().deleteCurrentUserFromChatRoom(id,
                    object : LiveLikeCallback<Boolean>() {
                        override fun onResponse(result: Boolean?, error: String?) {
                            result?.let {
                                showToast("Deleted ChatRoom")                     
                            }
                        }
                    })
```
```java
sdk.chat().deleteCurrentUserFromChatRoom(id,
                    new LiveLikeCallback<boolean>() {
                        	@override 
                          void onResponse(boolean result,String error) {
                           
                        }
                    });
```

## Add new member to chat room

Use this method to add other users to chat rooms.

```kotlin
sdk.chat().addUserToChatRoom(chatRoomId,
                userId,
                object : LiveLikeCallback<ChatRoomMembership>() {
                    override fun onResponse(result: ChatRoomMembership?, error: String?) {
                        result?.let {
                            showToast("User Added Successfully")
                        }
                       
                        error?.let {
                            showToast(it)
                        }
                       
                    }
                })
```

##
