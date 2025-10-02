---
title: iOS SDK
excerpt: Get a basic integration up and running with the iOS SDK
deprecated: false
hidden: false
metadata:
  title: Basic Integration | iOS SDK | LiveLike Developer Hub
  description: >-
    Get started on a basic integration with the LiveLike iOS SDK by going
    through our installation instructions. Learn more.
  robots: index
next:
  description: ''
---
This is a developers' guide for setting up a LiveLike SDK configuration for native iOS apps. We will take you through the basic technical steps for configuration and show you how to send your first widgets and chat messages. We will also provide detailed samples and instructions for a complete LiveLike integration.

## Prerequisites

* An admin login and registered application on the [Producer Suite](https://cf-blast.livelikecdn.com/) (provided by LiveLike).
* Client ID - Used to initialize the SDK. See instructions for [retrieving Your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).
* OS: iOS 10+

<Callout icon="📘" theme="info">
  Even though this guide makes use of both the chat and widget components, if desired it is possible to use only one of the components.
</Callout>

## Installation

The SDK can be installed via Swift Package Manager (recommended) or through package managers like [Carthage](https://livelike.readme.io/docs/ios-basic-integration#section-carthage) or [Cocoapods](https://livelike.readme.io/docs/ios-basic-integration#section-cocoapods).

## Swift Package Manager (versions 2.43.0+)

1. Open your project inside of Xcode and navigate to File > Add Packages...
2. Search for `https://bitbucket.org/livelike/livelike-ios-sdk.git` and select the `livelike-ios-sdk` swift package
3. Use the `Up to Next Major Version` dependency rule spanning from `2.0.0 < 3.0.0`, and hit the Add Package button

## CocoaPods

[https://guides.cocoapods.org/using/using-cocoapods.html](https://guides.cocoapods.org/using/using-cocoapods.html)

Add the following to a Podfile:

```text Podfile
target '<application-target-name>' do
    use_frameworks!
    pod 'EngagementSDK'
end
```

## Initialization

For this step, you will need your Client ID to initialize the Engagement SDK. To get your ClientID, follow the instructions in [Retrieving your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).

Import the EngagementSDK:

```swift
import EngagementSDK
```

Next, create an instance of the EngagementSDK.

If your billing is determined by *Monthly Active Users (MAUs)*, then at this point it is important to consider how and when the EngagementSDK will be initialized.

By default, the EngagementSDK will generate a new [User Profile](doc:user-profiles) upon first initialization. The Access Token of the User Profile will be stored in User Defaults and may not persist across app installations, devices, and/or platforms. We recommend that you override this default behavior and manage where the User's Access Token is stored. Find out how [here](doc:ios-user-profiles).

We also recommend that you initialize the SDK as late as possible in your application - just before the user accesses the EngagementSDK features.

<Callout icon="🚧" theme="warn">
  Concurrent instances of the EngagementSDK are not supported; only one instance should exist at any given time.
</Callout>

Use your Client ID to create a EngagementSDKConfig. The EngagementSDKConfig is used to initialize the EngagementSDK.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate {
  var engagementSDK: EngagementSDK!
  
  func application(_: UIApplication, didFinishLaunchingWithOptions _: [UIApplication.LaunchOptionsKey: Any]?) -> Bool { 
    var config = EngagementSDKConfig(clientID: "<your-client-id>")
    engagementSDK = EngagementSDK(config: config)  
    return true
  }
}
```

## Configure Your Layout

<Callout icon="📘" theme="info">
  Even though this guide makes use of both the chat and widget components, if desired it is possible to use only one of the components.
</Callout>

### Storyboards / XIB

If you are using the user interface to build your UI, then you need to add two UIViews to your view hierarchy for **Widget** and **Chat**. Add any constraints for managing the size and position of the subviews. Then, create and hook up an `@IBOutlet` in your ViewController for each view called `widgetView` and `chatView`.

```swift
class ViewController: UIViewController {
  @IBOutlet var widgetView: UIView!
  @IBOutlet var chatView: UIView!

  let widgetViewController = WidgetPopupViewController()
  let chatViewController = ChatViewController()
  
  override func viewDidLoad() {
      super.viewDidLoad()

      // Add `chatViewController` as child view controller
      addChild(chatViewController)
      chatViewController.didMove(toParent: self)

      // Apply constraints to the `chatViewController.view`
      chatViewController.view.translatesAutoresizingMaskIntoConstraints = false
      chatView.addSubview(chatViewController.view)
      NSLayoutConstraint.activate([
          chatViewController.view.topAnchor.constraint(equalTo: chatView.topAnchor),
          chatViewController.view.trailingAnchor.constraint(equalTo: chatView.trailingAnchor),
          chatViewController.view.leadingAnchor.constraint(equalTo: chatView.leadingAnchor),
          chatViewController.view.bottomAnchor.constraint(equalTo: chatView.bottomAnchor)
      ])

      // Add `widgetViewController` as child view controller
      addChild(widgetViewController)
      widgetViewController.didMove(toParent: self)

      // Apply constraints to the `widgetViewController.view`
      widgetViewController.view.translatesAutoresizingMaskIntoConstraints = false
      widgetView.addSubview(widgetViewController.view)
      NSLayoutConstraint.activate([
          widgetViewController.view.topAnchor.constraint(equalTo: widgetView.topAnchor),
          widgetViewController.view.trailingAnchor.constraint(equalTo: widgetView.trailingAnchor),
          widgetViewController.view.leadingAnchor.constraint(equalTo: widgetView.leadingAnchor),
          widgetViewController.view.bottomAnchor.constraint(equalTo: widgetView.bottomAnchor)
      ])
  }
}
```

<Callout icon="🚧" theme="warn">
  If you are working in a multilayered UIView environment where the `widgetView` is placed above the `chatView`. It is best practice to instantiate the `widgetView` as `PassthroughView`. This will allow user interactions on `widgetView` effect the `chatView` when there are no activate widgets.
</Callout>

### Programmatic

In your ViewController, create an instance of `WidgetPopupViewController` and `ChatViewController`

<Callout icon="🚧" theme="warn">
  Important: The width of the Widget view must be at least 260 and height 280. The width of the Chat view must be at least 292.
</Callout>

Add the `WidgetViewController` and `ChatViewController` as a child view controller to your ViewController. For more information on child view controllers see Apple documentation on [Implementing a ContainerViewController](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/ImplementingaContainerViewController.html).

In the `viewDidLoad` method add the following constraints:

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    // Add `chatViewController` as child view controller
    addChild(chatViewController)
    chatViewController.didMove(toParent: self)

    // Apply constraints to the `chatViewController.view`
    chatViewController.view.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(chatViewController.view)
    NSLayoutConstraint.activate([
        chatViewController.view.topAnchor.constraint(equalTo: view.topAnchor),
        chatViewController.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
        chatViewController.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
        chatViewController.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
    ])

    // Add `widgetViewController` as child view controller
    addChild(widgetViewController)
    widgetViewController.didMove(toParent: self)

    // Apply constraints to the `widgetViewController.view`
    widgetViewController.view.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(widgetViewController.view)
    NSLayoutConstraint.activate([
        widgetViewController.view.topAnchor.constraint(equalTo: view.topAnchor),
        widgetViewController.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
        widgetViewController.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
        widgetViewController.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
    ])
}
```

## Start a Content Session

A Content Session represents a user's subscription to a particular <Glossary>Program</Glossary> (typically a live, linear TV show, game or episode). To start a Content Session you will need a **Program ID**. You will need to create programs within the LiveLike system, either through the API or through the [Producer Suite](https://cf-blast.livelikecdn.com/) (see [Getting Started with the Producer Suite](doc:ps-getting-started)). You should then copy the **Program ID**s into the relevant media metadata in your own systems, so that content sessions can be started along with media playback.

Use the following resources to get started with the Producer Suite

* [Creating a Program](https://docs.livelike.com/docs/ps-getting-started#section-creating-a-program)
* [Retrieving a Program ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-program-id)
* [Publishing a Widget](https://docs.livelike.com/docs/ps-getting-started#section-publishing-widgets)

In your ViewController, declare a variable to maintain an instance of the `ContentSession` we will be creating.

<Callout icon="🚧" theme="warn">
  Important: A reference to the `ContentSession` instance must be maintained in order for the session to remain valid and receive Widget and Chat events.
</Callout>

```swift
class ViewController: UIViewController {
    @IBOutlet var widgetView: UIView!
    @IBOutlet var chatView: UIView!

    let widgetViewController = WidgetPopupViewController()
    let chatViewController = ChatViewController()

    var session: ContentSession?
}
```

Now call the contentSession method of your instance of the EngagementSDK - passing in your **Program ID**. This will return a `ContentSession` object. You must store this in the `ContentSession` variable declared earlier.

Assign the ContentSession to the WidgetPopupViewController so the user can begin receiving widgets published from the CMS.

Assign the ContentSession to the ChatViewController so the user will also be able to participate in the chat room.

```swift
func startContentSession(engagementSDK: EngagementSDK) {
    let config = SessionConfiguration(programID: "<program-id>")
    session = engagementSDK.contentSession(config: config)
    widgetViewController.session = session
    chatViewController.session = session
}
```
```objectivec
- (*void*)startContentSession: (LLEngagementSDK*)engagementSDK {
    LLSessionConfiguration *config = [[LLSessionConfiguration alloc] initWithProgramID:@"<program-id>"];                  
    id<LLContentSession> session = [engagementSDK contentSessionWithConfig:config];
    self.session = session;
    chatViewController.session = session;
    widgetViewController.session = session;
}
```

## Close a Content Session

When the user returns to your application's home page and away from your live video screen you will want to **close** the ContentSession. Closing a session will disconnect from Widgets and Chat and release all the related resources.

<Callout icon="📘" theme="info">
  You can also set the session reference to `nil`, this is the same as calling close
</Callout>

```swift
override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(animated)
    self.session?.close()
    //or
    self.session = nil
}
```

## Sample Integration

The following is a summary of what the steps above look like when taken together:

```swift
import UIKit
import EngagementSDK

class ViewController: UIViewController {

    @IBOutlet weak var widgetView: UIView!
    @IBOutlet weak var chatView: UIView!

    var engagementSDK: EngagementSDK!

    //Creating the Widget and Chat ViewControllers
    let widgetViewController = WidgetPopupViewController()
    let chatViewController = ChatViewController()

    //Holding a reference to the session to keep it valid
    var session: ContentSession?
    
    override func viewDidLoad() {
        super.viewDidLoad()

        var sdkConfig = EngagementSDKConfig(clientID: "<your-client-id>")
        engagementSDK = EngagementSDK(config: sdkConfig)
        
        // Adding widgetViewController as child view controller
        addChild(widgetViewController)
        widgetView.addSubview(widgetViewController.view)
        widgetViewController.didMove(toParent: self)
        
        // Applying constraints to fill the container
        widgetViewController.view.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            widgetViewController.view.bottomAnchor.constraint(equalTo: widgetView.bottomAnchor),
            widgetViewController.view.topAnchor.constraint(equalTo: widgetView.topAnchor),
            widgetViewController.view.trailingAnchor.constraint(equalTo: widgetView.trailingAnchor),
            widgetViewController.view.leadingAnchor.constraint(equalTo: widgetView.leadingAnchor)
            ])
        
        // Adding chatViewController as a child view controller
        addChild(chatViewController)
        chatView.addSubview(chatViewController.view)
        chatViewController.didMove(toParent: self)
        
        // Applying constraints to fill the container
        chatViewController.view.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            chatViewController.view.bottomAnchor.constraint(equalTo: chatView.bottomAnchor),
            chatViewController.view.topAnchor.constraint(equalTo: chatView.topAnchor),
            chatViewController.view.trailingAnchor.constraint(equalTo: chatView.trailingAnchor),
            chatViewController.view.leadingAnchor.constraint(equalTo: chatView.leadingAnchor)
            ])

        //Creating a Content Session
        let config = SessionConfiguration(programID: "<program-id>")
        session = engagementSDK.contentSession(config: config)
        session.delegate = self

       // Applying the Content Session to the Widget and Chat ViewControllers
        widgetViewController.session = session
        chatViewController.session = session
    }

    //Ending a session
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        self.session?.close()
    }
}
```