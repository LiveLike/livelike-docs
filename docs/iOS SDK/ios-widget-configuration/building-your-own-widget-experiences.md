---
title: Building Your Own Widget Experiences
excerpt: A guide on how to use the EngagementSDK to build your own Widget experiences.
deprecated: false
hidden: false
metadata:
  title: Building Your Own Widget Experiences | iOS SDK | LiveLike
  description: >-
    A guide on how to use the Engagement SDK to build your own widget
    experiences. Learn more about display widgets, realtime widgets, and more.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "What you'll need to know",
  "body": "1. Creating the EngagementSDK instance\n2. Creating a ContentSession"
}
[/block]
We provide the WidgetPopupViewController out of the box for a user experience curated by our design team and for a simple integration into your application - but the WidgetPopupViewController doesn't showcase all the ways that Widgets can be used!

Maybe you want to show a list view of past widgets, or maybe have a running poll throughout an event, or maybe...

In this guide you'll learn how to:
1. Get and display widgets on demand in your layout
2. Control the lifecycle of the widgets
[block:api-header]
{
  "title": "Get and Display Widgets"
}
[/block]
**There are 3 different methods of getting widgets to show in your hierarchy:**
1. Subscribing to Realtime Widgets being published by the Producer
2. Get a list or a single Widget that has already been published
3. Using a compatible JSON representation of a Widget

The `Widget` is a `UIViewController` so you will be able to add it to your view hierarchy like any `UIViewController`.
[block:api-header]
{
  "title": "Subscribing to Realtime Widgets"
}
[/block]
Using a Content Session you can subscribe to Widgets that are being published by the Producer. Implement the `widget(session: didBecomeReady:)` method of the ContentSessionDelegate.
[block:callout]
{
  "type": "warning",
  "title": "Considerations with the WidgetPopupViewController",
  "body": "The WidgetPopupViewController will override the ContentSession's delegate with itself. Custom Widget experiences are not simultaneously compatible with the same ContentSession."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  \n  let sdk: EngagementSDK!\n  let session: ContentSession!\n  \n  func someMethod() {\n    let sessionConfig = SessionConfiguration(programID: \"program-id\")\n    session = sdk.contentSession(config: sessionConfig)\n    session.delegate = self\n  }\n}\n\nextension SomeClass: ContentSessionDelegate {\n\t// Called when the Producer publishes a widget\n\tfunc widget(_ session: ContentSession, didBecomeReady widget: Widget) {\n\t\t// Do something with Widget\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Published Widgets"
}
[/block]
Using a Content Session you can retrieve a paginated list of Widgets (up to 20 per page) that have already been published using the getPostedWidgets(page: completion:) method. You can pass `.first` or `.next` as `page`. 

`.first` will always return the newest Widgets.
`.next` will return the next page from the oldest page loaded.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  var contentSession: ContentSession!\n  \n  func someMethod() {\n    contentSession.getPostedWidgets(page: .first) { [weak self] result in\n      guard let self = self else { return }\n      switch result {\n        case .success(let widgets):\n          // widgets == nil if there are no posted widgets\n          // Do something with widgets\n        case .failure(let error):\n          // Something went wrong\n      }\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get a Published Widget"
}
[/block]
As an integrator you have the ability to query our backend for a specific widget to either display it to the user right away or save the widget details for later use (coming soon). In order to retrieve a `Widget` you will need to know it's `id` and `kind` and use the `func getWidget(id: String, kind: WidgetKind, completion: @escaping (Result<Widget, Error>) -> Void)` function.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  \n  let sdk: EngagementSDK!\n  let session: ContentSession!\n  \n  func someMethod() {\n    sdk = EngagementSDK(config: EngagementSDKConfig(clientID:\"<client id>\"))\n    sdk.getWidget(id: \"<widget id>\", kind: <widget kind>) {     \n \n      result in guard let self = self else { return }\n      switch result {\n        case .success(let widget):\n          // present `Widget` to your user\n        case .failure(let error):\n          // Something went wrong\n      }\n  }\n}",
      "language": "swift",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Instantiate Widget From JSON"
}
[/block]
If you're interacting with our REST API directly or if you have a stored widget JSON that you wish to display then you will need to instantiate that Widget using the `createWidgets(widgetJSONObjects:completion)` method in EngagementSDK. This will take your JSON Object and return the Widget to be displayed.
[block:callout]
{
  "type": "info",
  "title": "JSON Object",
  "body": "The JSON Object must be compatible with `JSONSerialization.data(jsonObject:options:)`. You may want to use `JSONSerialization.isValidJSONObject(obj:)` to verify a valid JSON Object."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  var engagement: EngagementSDK!\n  let widgetJSONObject: Any // The Widget JSON Object from REST API\n  \n  func someMethod() {\n    engagement.createWidgets(widgetJSONObjects: [widgetJSONObject]) { [weak self] result in\n      guard let self = self else { return }\n      switch result {\n        case .success(let widgets):\n          // Do something with widgets\n        case .failure(let error):\n          // Failed to parse Widgets from JSON Object\n      }\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
Using a Content Session you can subscribe to Widgets that are being published by the Producer. 
[block:api-header]
{
  "title": "Managing the Widget Lifecycle"
}
[/block]
The widgets operate under these four states (in order):
1. Ready
2. Interactive
3. Results
4. Finished

**Caveats:**
* Ready state cannot be 'Entered`. A widget starts in the Ready state.
* Alerts don't use the Results state

You can manage the widget lifecycle by observing the state changes and controlling when the widget will move to the next state. 

**The lifecycle events are:**
* Widget entering a state - The widget has entered this state
* Widget can complete a state - The widget has completed all delayed processes (ie. Network Requests and Animations)

To observe the lifecycle events implement the `WidgetEvents` protocol and set as the delegate to a `WidgetViewModel`

To make the widget move to the next state call `moveToNextState()` on a `WidgetViewModel`
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass: WidgetEvents {\n\tfunc widgetDidEnterState(widget: WidgetViewModel, state: WidgetState){\n    switch state {\n      case .ready:\n      \t// This state cannot be `entered` and this will never be called.\n      \tbreak\n      case .interactive:\n      \t// Handle entering the interactive state (eg. Begin a timer)\n      \t// Then maybe move to the next state\n      \twidget.moveToNextState()\n      case .results:\n      \t// Handle entering the results state\n      case .finished:\n      \t// Handle entering the finished state (eg. Hiding the widget)\n    }\n  }\n  \n \tfunc widgetStateCanComplete(widget: WidgetViewModel, state: WidgetState){\n    switch state {\n      case .ready:\n      \t// This state cannot be `completed` and this will never be called.\n      \tbreak\n      case .interactive:\n      \t// Handle the interactive state 'completing'\n      case .results:\n      \t// Handle the results state 'completing'\n      case .finished:\n\t\t\t\t// Handle the finished state 'completing'\n    }\n  }\n}",
      "language": "swift",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Subscribe to Widget Interactions"
}
[/block]
Widget interactions are a useful event to show additional UI or to trigger widget state changes. For an example, you may want to move a Quiz widget into the results state immediately after the user has selected an option.

An interaction is defined for each widget as:
**Poll**: User selects any option
**Quiz**: User selects any option
**Prediction**: User selects any option
**Prediction Follow Up**: n/a
**Cheer Meter**: User selects any option
**Image Slider**: User releases the slider knob
**Alert**: User opens link


[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n  \n  private let widget: WidgetViewModel\n  \n  func viewDidLoad() {\n    super.viewDidLoad()\n    widget.delegate = self\n  }\n}\n\nextension MyViewController: WidgetViewDelegate {\n  func userDidInteract(_ widget: WidgetViewModel) {\n    // do something\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]