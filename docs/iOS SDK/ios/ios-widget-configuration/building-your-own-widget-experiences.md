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
> 📘 What you'll need to know
>
> 1. Creating the EngagementSDK instance
> 2. Creating a ContentSession

We provide the WidgetPopupViewController out of the box for a user experience curated by our design team and for a simple integration into your application - but the WidgetPopupViewController doesn't showcase all the ways that Widgets can be used!

Maybe you want to show a list view of past widgets, or maybe have a running poll throughout an event, or maybe...

In this guide you'll learn how to:

1. Get and display widgets on demand in your layout
2. Control the lifecycle of the widgets

## Get and Display Widgets

**There are 3 different methods of getting widgets to show in your hierarchy:**

1. Subscribing to Realtime Widgets being published by the Producer
2. Get a list or a single Widget that has already been published
3. Using a compatible JSON representation of a Widget

The `Widget` is a `UIViewController` so you will be able to add it to your view hierarchy like any `UIViewController`.

## Subscribing to Realtime Widgets

Using a Content Session you can subscribe to Widgets that are being published by the Producer. Implement the `widget(session: didBecomeReady:)` method of the ContentSessionDelegate.

> 🚧 Considerations with the WidgetPopupViewController
>
> The WidgetPopupViewController will override the ContentSession's delegate with itself. Custom Widget experiences are not simultaneously compatible with the same ContentSession.

```swift
class SomeClass {
  
  let sdk: EngagementSDK!
  let session: ContentSession!
  
  func someMethod() {
    let sessionConfig = SessionConfiguration(programID: "program-id")
    session = sdk.contentSession(config: sessionConfig)
    session.delegate = self
  }
}

extension SomeClass: ContentSessionDelegate {
	// Called when the Producer publishes a widget
	func widget(_ session: ContentSession, didBecomeReady widget: Widget) {
		// Do something with Widget
  }
}
```

## Get Published Widgets

Using a Content Session you can retrieve a paginated list of Widgets (up to 20 per page) that have already been published using the getPostedWidgets(page: completion:) method. You can pass `.first` or `.next` as `page`. 

`.first` will always return the newest Widgets.\
`.next` will return the next page from the oldest page loaded.

```swift
class SomeClass {
  var contentSession: ContentSession!
  
  func someMethod() {
    contentSession.getPostedWidgets(page: .first) { [weak self] result in
      guard let self = self else { return }
      switch result {
        case .success(let widgets):
          // widgets == nil if there are no posted widgets
          // Do something with widgets
        case .failure(let error):
          // Something went wrong
      }
    }
  }
}
```

## Get a Published Widget

As an integrator you have the ability to query our backend for a specific widget to either display it to the user right away or save the widget details for later use (coming soon). In order to retrieve a `Widget` you will need to know it's `id` and `kind` and use the `func getWidget(id: String, kind: WidgetKind, completion: @escaping (Result<Widget, Error>) -> Void)` function.

```swift
class SomeClass {
  
  let sdk: EngagementSDK!
  let session: ContentSession!
  
  func someMethod() {
    sdk = EngagementSDK(config: EngagementSDKConfig(clientID:"<client id>"))
    sdk.getWidget(id: "<widget id>", kind: <widget kind>) {     
 
      result in guard let self = self else { return }
      switch result {
        case .success(let widget):
          // present `Widget` to your user
        case .failure(let error):
          // Something went wrong
      }
  }
}
```

## Instantiate Widget From JSON

If you're interacting with our REST API directly or if you have a stored widget JSON that you wish to display then you will need to instantiate that Widget using the `createWidgets(widgetJSONObjects:completion)` method in EngagementSDK. This will take your JSON Object and return the Widget to be displayed.

> 📘 JSON Object
>
> The JSON Object must be compatible with `JSONSerialization.data(jsonObject:options:)`. You may want to use `JSONSerialization.isValidJSONObject(obj:)` to verify a valid JSON Object.

```swift
class SomeClass {
  var engagement: EngagementSDK!
  let widgetJSONObject: Any // The Widget JSON Object from REST API
  
  func someMethod() {
    engagement.createWidgets(widgetJSONObjects: [widgetJSONObject]) { [weak self] result in
      guard let self = self else { return }
      switch result {
        case .success(let widgets):
          // Do something with widgets
        case .failure(let error):
          // Failed to parse Widgets from JSON Object
      }
    }
  }
}
```

Using a Content Session you can subscribe to Widgets that are being published by the Producer. 

## Managing the Widget Lifecycle

The widgets operate under these four states (in order):

1. Ready
2. Interactive
3. Results
4. Finished

**Caveats:**

* Ready state cannot be 'Entered\`. A widget starts in the Ready state.
* Alerts don't use the Results state

You can manage the widget lifecycle by observing the state changes and controlling when the widget will move to the next state. 

**The lifecycle events are:**

* Widget entering a state - The widget has entered this state
* Widget can complete a state - The widget has completed all delayed processes (ie. Network Requests and Animations)

To observe the lifecycle events implement the `WidgetEvents` protocol and set as the delegate to a `WidgetViewModel`

To make the widget move to the next state call `moveToNextState()` on a `WidgetViewModel`

```swift
class SomeClass: WidgetEvents {
	func widgetDidEnterState(widget: WidgetViewModel, state: WidgetState){
    switch state {
      case .ready:
      	// This state cannot be `entered` and this will never be called.
      	break
      case .interactive:
      	// Handle entering the interactive state (eg. Begin a timer)
      	// Then maybe move to the next state
      	widget.moveToNextState()
      case .results:
      	// Handle entering the results state
      case .finished:
      	// Handle entering the finished state (eg. Hiding the widget)
    }
  }
  
 	func widgetStateCanComplete(widget: WidgetViewModel, state: WidgetState){
    switch state {
      case .ready:
      	// This state cannot be `completed` and this will never be called.
      	break
      case .interactive:
      	// Handle the interactive state 'completing'
      case .results:
      	// Handle the results state 'completing'
      case .finished:
				// Handle the finished state 'completing'
    }
  }
}
```

## Subscribe to Widget Interactions

Widget interactions are a useful event to show additional UI or to trigger widget state changes. For an example, you may want to move a Quiz widget into the results state immediately after the user has selected an option.

An interaction is defined for each widget as:\
**Poll**: User selects any option\
**Quiz**: User selects any option\
**Prediction**: User selects any option\
**Prediction Follow Up**: n/a\
**Cheer Meter**: User selects any option\
**Image Slider**: User releases the slider knob\
**Alert**: User opens link

```swift
class MyViewController: UIViewController {
  
  private let widget: WidgetViewModel
  
  func viewDidLoad() {
    super.viewDidLoad()
    widget.delegate = self
  }
}

extension MyViewController: WidgetViewDelegate {
  func userDidInteract(_ widget: WidgetViewModel) {
    // do something
  }
}
```
