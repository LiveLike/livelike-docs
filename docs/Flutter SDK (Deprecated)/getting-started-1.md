---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Getting Started | Flutter SDK | LiveLike Developer Hub
  description: >-
    This is a developers' guide for setting up a LiveLike SDK configuration for
    flutter apps. Learn more about the LiveLike Flutter SDK.
  robots: index
next:
  description: ''
---
This is a developers' guide for setting up a LiveLike SDK configuration for Flutter apps. We will take you through the basic technical steps for configuration and show you how to send your first chat messages. The LiveLike Flutter SDK  depends on the native SDK of LiveLike, it uses Embedded PlatformView and UiKitView to View the widgets and chats features in Flutter. For communication between the Flutter and native platforms, we use the event channel supported by Flutter SDK itself.

> ❗️ Flutter is not supported.
> 
> The Flutter SDK is not actively maintained and is not supported.

> 🚧 LiveLike Flutter SDK
> 
> The SDK currently supports only the Android(**LiveLike SDK 2.23.2**) and IOS(**LiveLike SDK 2.29.1**) platform.

## Installation

Add below lines to your pubspec.yaml under dependencies.

> 👍 Flutter LiveLike SDK
> 
> livelike_flutter_sdk: ^0.2.0

Check Pub Dev Link for more details: <https://pub.dev/packages/livelike_flutter_sdk>

## Initialization

For this step, you will need your Client ID to initialize the Engagement SDK. To get your ClientID, follow the instructions in [Retrieving your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).

Use ClientId to create the EngagementSDK instance.

```text Dart
final sdk = EngagementSDK("<client-id>");
```

**Access Token**

The LiveLike SDK generates a User <<glossary: Access Token>> whenever initialized. You can either choose to store it locally or persist it within your internal user database (although we have already managed it internally in the SDK). The access Token is stored locally which can be updated if the user uninstalls the application or clears data from application settings. This may result in higher MAUs([Monthly Active Users], so it is highly recommended to pass the accessToken delegate as a param on SDK init and store the accessToken for persistent users count.

To Use the EngagementSDK instance with the accessToken.

```text Dart
EngagementSDK.accessToken("<client-id>",
            <access-token>,(accessToken){
            // Receive the latest access Token
            })
```

In Order to get the accessToken for the first when a new user is created.

**Note**: AccessTokenStream can only be used with EngagementSDK.accessToken constructor else it will give the issue related "**No Implementation Found**"

> ❗️ AccessTokenStream
> 
> AccessTokenStream is removed from 0.0.2, added a delegate method in the EngagementSDK.accessToken constructor

## Chat Session

A Chat Session represents a connection to a Chat Room. You can read and interact with a Chat Room via a Chat Session.

**Create Chat Session**

Connecting to a chat room creates a ChatSession object which represents the connection. While this object exists the ChatSession will remain connected.

```text Dart
final session =await sdk.createChatSession(<chat-room-id>)
```

**Pause/Resume Chat Session**

To make the services related to chat of LiveLike pause and resume.

```text Dart
session.resume();
session.pause();
```

**Close Chat Session**  
To close the chat services in LiveLike SDK and clear all variables.

```text Dart
session.close();
```

## Content Session

A Content Session represents a connection to a Widget Interaction System. You can receive and vote on the widget. 

**Create Content Session**

Connecting to a widget interaction system creates a ContentSession object which represents the connection. While this object exists the ContentSession will remain connected.

```text Dart
final session = await sdk.createSession(<program-id>);
```

**Pause/Resume Content Session**

To make the services related to widgets of LiveLike pause and resume.

```text Dart
session.resume();
session.pause();
```

**Close Content Session**  
To close the widget services in LiveLike SDK and clear all variables.

```text Dart
session.close();
```

**To fetch List of Posted Widgets for a given Program**

```text Dart
final list = await session?.getPublishedWidgets(LiveLikePagination.first);
```

**LiveLikePagination**  
the LiveLikePagination enum is used for lazy loading, right now by default widgets loaded a limit of 20, in order to start the call the api with LiveLikePagination.first which will return you first page data and call api with LiveLikePagination.next which will get next page data and similarly LiveLikePagination.previous will get previous page data, in next once you get the empty array you have reached the last page.

## Programs

To fetch the list of Programs associated with an Application.

```text Dart
final programList =  await sdk.fetchListOfProgram(pagination)
```

To fetch the program details based on programId.

```text Dart
final program = await sdk.fetchProgram(programId)
```

## Change Nick Name

To update the nickname of the user-created, the name updated is shown in the ChatView ,Leaderboard etc

```kotlin Dart
await sdk.updateNickName(name);
 name = await sdk.getNickName();
```