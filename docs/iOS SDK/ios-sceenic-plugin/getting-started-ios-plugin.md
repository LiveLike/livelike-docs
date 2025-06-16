---
title: Getting Started with Sceenic (iOS)
excerpt: Get a basic integration up and running with the iOS Sceenic Video Plugin
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This is a developers' guide for setting up a Sceenic Video Plugin configuration for native iOS apps. We will take you through the basic technical steps for configuration and show you how to create video rooms and initiate video calls.
[block:api-header]
{
  "title": "Prerequisites"
}
[/block]
* An admin login and registered application on the [Producer Suite](http://producer.livelikecdn.com/) (provided by LiveLike).
* Client ID - Used to initialize the Plugin. See instructions for [retrieving Your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).
* OS: iOS 11+
[block:api-header]
{
  "title": "Installation"
}
[/block]
The Plugin can be installed via Cocoapods.

https://guides.cocoapods.org/using/using-cocoapods.html

Add the following to a Podfile:
[block:code]
{
  "codes": [
    {
      "code": "target '<application-target-name>' do\n    use_frameworks!\n    pod 'LiveLikeSceenicVideoPlugin'\nend",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Initialization"
}
[/block]
For this step, you will need your Client ID to initialize the Engagement SDK. To get your ClientID, follow the instructions in [Retrieving your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).

Import the LiveLikeSceenicVideoPlugin:
[block:code]
{
  "codes": [
    {
      "code": "import LiveLikeSceenicVideoPlugin",
      "language": "swift"
    }
  ]
}
[/block]
Next, create an instance of the LiveLikeSceenicVideoPlugin.

The Access Token of the User will be stored in User Defaults and may not persist across app installations, devices, and/or platforms. We recommend that you override this default behavior and manage where the User's Access Token is stored.

Use your Client ID to create a LiveLikeSceenicPluginConfig. The LiveLikeSceenicPluginConfig is used to initialize the LiveLikeSceenicVideoPlugin.
[block:code]
{
  "codes": [
    {
      "code": "class AppDelegate: UIResponder, UIApplicationDelegate {\n  var sceenicPlugin: LiveLikeSceenicVideoPlugin!\n  \n  func application(_: UIApplication, didFinishLaunchingWithOptions _: [UIApplication.LaunchOptionsKey: Any]?) -> Bool { \n    var config = LiveLikeSceenicPluginConfig(clientID: \"<your-client-id>\")\n    sceenicPlugin = LiveLikeSceenicVideoPlugin(config: config)  \n    return true\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]