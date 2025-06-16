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

## Spoiler Prevention using ContentSession

When working with `ContentSession` you can enable spoiler prevention by setting `SessionConfiguration.syncTimeSource` to your `AVPlayer.programDateTime` 

```swift
class ViewController: UIViewController{
    var session: ContentSession?
    
    override func viewDidLoad(){
        let config = SessionConfiguration(
            programID: <"program id">,
            chatHistoryLimit: 50,
            widgetConfig: WidgetConfig()
        )
        config.syncTimeSource = { [weak self] in
            self?.videoPlayer.player?.programDateTime.timeIntervalSince1970
        }
        
        session = sdk.contentSession(config: config)
        chatViewController.session = session
        widgetViewController.session = session
    }
}
```

## Spoiler Prevention using ChatSession

When working with `ChatSession` you can enable spoiler prevention by setting the `ChatSessionConfig.syncTimeSource` variable. 

```swift
let sdk: EngagementSDK
var config = ChatSessionConfig(roomID: chatRoomId)
config.syncTimeSource = { [weak self] in
                         self?.avPlayer.player?.programDateTime.timeIntervalSince1970
                        }
sdk.connectChatRoom(config: config,
                    completion: { [weak self] result in
                                 DispatchQueue.main.async {
                                     guard let self = self else { return }
                                     switch result {
                                         case let .success(chatSession):
                                         self.chatViewController.setChatSession(chatSession)
                                         case let .failure(error):
                                         print(error)
                                     }
                                 }
                                })
```
