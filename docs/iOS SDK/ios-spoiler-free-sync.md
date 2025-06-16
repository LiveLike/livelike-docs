---
title: Spoiler Prevention (iOS)
excerpt: Preventing spoilers on iOS
deprecated: false
hidden: false
metadata:
  title: Spoiler Prevention | iOS SDK | LiveLike Developer Hub
  description: >-
    Our iOS Spoiler Prevention feature enables you to publish spoiler-free
    content with the Engagement SDK. Learn more.
  robots: index
next:
  description: ''
---
This feature enables you to publish spoiler-free content with the Engagement SDK. When enabled, all published content from the Producer Suite and chat messages will be synced with the live video (we don't currently support VOD). 

To enable Spoiler Prevention, you will need to provide a value that represents the date/time of your media player's current playback position. 

If you are using **AVPlayer** and streams that support the [EXT-X-PROGRAM-DATE-TIME](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23#section-4.3.2.6) tag, we provide an AVPlayer extension in the EngagementSDK to allow you to quickly enable Spoiler Prevention. Simply, return the **programDateTime** property of your AVPlayer instance, which will extract the reference date from supported stream types. See the samples below.

Otherwise, if you're using a different player or need to calculate the reference time using a different strategy, you will need to return your custom date/time as a **Date** object.
[block:api-header]
{
  "title": "Spoiler Prevention using ContentSession"
}
[/block]
When working with `ContentSession` you can enable spoiler prevention by setting `SessionConfiguration.syncTimeSource` to your `AVPlayer.programDateTime` 
[block:code]
{
  "codes": [
    {
      "code": "class ViewController: UIViewController{\n    var session: ContentSession?\n    \n    override func viewDidLoad(){\n        let config = SessionConfiguration(\n            programID: <\"program id\">,\n            chatHistoryLimit: 50,\n            widgetConfig: WidgetConfig()\n        )\n        config.syncTimeSource = { [weak self] in\n            self?.videoPlayer.player?.programDateTime.timeIntervalSince1970\n        }\n        \n        session = sdk.contentSession(config: config)\n        chatViewController.session = session\n        widgetViewController.session = session\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Spoiler Prevention using ChatSession"
}
[/block]
When working with `ChatSession` you can enable spoiler prevention by setting the `ChatSessionConfig.syncTimeSource` variable. 
[block:code]
{
  "codes": [
    {
      "code": "let sdk: EngagementSDK\nvar config = ChatSessionConfig(roomID: chatRoomId)\nconfig.syncTimeSource = { [weak self] in\n                         self?.avPlayer.player?.programDateTime.timeIntervalSince1970\n                        }\nsdk.connectChatRoom(config: config,\n                    completion: { [weak self] result in\n                                 DispatchQueue.main.async {\n                                     guard let self = self else { return }\n                                     switch result {\n                                         case let .success(chatSession):\n                                         self.chatViewController.setChatSession(chatSession)\n                                         case let .failure(error):\n                                         print(error)\n                                     }\n                                 }\n                                })",
      "language": "swift"
    }
  ]
}
[/block]