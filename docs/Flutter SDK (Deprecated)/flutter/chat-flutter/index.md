---
title: Chat View
excerpt: Showing livelike chatview in your flutter app
deprecated: false
hidden: false
metadata:
  title: Chat View | Flutter SDK | Chat Room | LiveLike
  description: >-
    To use the ChatView Widget in your Flutter app, add the ChatView Widget in
    your app and provide chatSession object to that widget.
  robots: index
next:
  description: ''
---
## Chat View

For using the ChatView Widget in your flutter app, you have to add the ChatView Widget in your app and provide chatSession object to that widget.

```text
ChatView(key: Key("${chatSession.chatRoomId}"), session: chatSession)
```

> 🚧 Note:
>
> If you are facing extra padding when keyboard appears in IOS, then add
> **resizeToAvoidBottomInset: !Platform.IOS,**
> attribute to your Scaffold to avoid this issue, and make sure it is true for android platform