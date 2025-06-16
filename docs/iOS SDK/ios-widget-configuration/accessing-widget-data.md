---
title: Accessing Widget Models
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Accessing Widget Data | iOS SDK | LiveLike Developer Hub
  description: >-
    This is an iOS guide on Widget Models as part of the Custom Widget UI
    system. Learn more about accessing widget data.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version",
  "body": "2.11"
}
[/block]
This is an iOS guide on Widget Models as part of the Custom Widget UI system. For an overview on Custom Widget UI see [Building Custom Widget UI](doc:custom-widget-ui).
[block:api-header]
{
  "title": "What are Widget Models?"
}
[/block]
Widget Models are representations of a Widget as it is on the server. Widget Models give you the access to read a Widget's data, submit votes, and observe changes to the Widget. Ultimately, a Widget Model provides everything for you to build Custom UI to support your use case. 

While each Widget has a unique Widget Model class that represents it, they are encapsulated under the WidgetModel enum *TODO LINK* in order to simplify the access methods. Use a `switch` statement on WidgetModel to get the exact Widget Model.

There are 3 ways to access/retrieve a Widget Model to support various use-cases. All 3 methods require a ContentSession. For more information on Content Session see [Getting Started](doc:ios-basic-integration). 
[block:api-header]
{
  "title": "Subscribing to Realtime Widget Models"
}
[/block]
Implement the ContentSessionDelegate to observe when a Widget is published by the Producer.
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n    \n  let session: ContentSession\n    \n  override func viewDidLoad() {\n    super.viewDidLoad()\n      \n    session.delegate = self\n  }\n}\n\nextension MyViewController: ContentSessionDelegate {\n  func contentSession(_ session: ContentSession, didReceiveWidget widgetModel: WidgetModel) {\n    switch widgetModel {\n     \t// Do something with widgetModel\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get a Widget Model by ID"
}
[/block]
If you know the widget id and kind you can choose to fetch the widget model from the server.
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n    \n  let session: ContentSession\n  let widgetID: String\n  let widgetKind: WidgetKind\n    \n  override func viewDidLoad() {\n  \tsuper.viewDidLoad()\n        \n    session.getWidgetModel(id: widgetID, kind: widgetKind) { result in\n   \t  switch result {\n      case .success(let widgetModel):\n  \t  \tswitch widgetModel {\n      \t  // Do something with widgetModel\n      \t}\n      case .failure(let error):\n      \t// handle error\n      }\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "`getWidgetModels()`",
  "body": "The `getWidgetModels()` SDK interface will be available in iOS SDK version 2.37"
}
[/block]

[block:api-header]
{
  "title": "Getting Widget Models"
}
[/block]
This method can be used to fetch a paginated result of Widgets Models filtered by the `options` parameter.
The request filters and sorts are defined in the `GetWidgetsRequestOptions` struct. 

The filtering options include:
* widgetKind - The set of widget kinds to include
* widgetStatus - The publishing status of the widget
* widgetOrdering - The order in which the widgets will be returned
* interactive - Filters for only widgets that can still be interacted with
* since - A Date parameter that filters out widgets with an earlier created date
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n    \n  let session: ContentSession\n    \n  override func viewDidLoad() {\n  \tsuper.viewDidLoad()\n    \n    let options = GetWidgetModelsRequestOptions(\n      widgetStatus: .published,\n      widgetKind: [.textPoll, .imagePrediction],\n      widgetOrdering: .recent\n    )\n    \n    session.getWidgetModels(\n      page: .first,\n      options: options\n    ) { result in\n       switch result {\n         case let .success(widgets):\n         case let .failure(error):\n       }\n      }    \n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Published Widget Models from History"
}
[/block]
For use-cases like a Timeline mode, you can perform a paginated fetch of the most recent widget models (~20) on the server. Call with `.first` to get the first page then you may call using `.next` for subsequent pages.
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n    \n  let session: ContentSession\n   \n  override func viewDidLoad() {\n    super.viewDidLoad()        \n        \n    session.getPostedWidgetModel(page: .first) { result in\n      switch result {\n      case .success(let widgetModels):\n      \tswitch widgetModel {\n      \t  // Do something with widgetModel\n      \t}\n     \tcase .failure(let error):\n        // handle error\n      }\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Interaction History"
}
[/block]
*Available in version 2.24*

For many use-cases you may be interested in loading the user's interaction history on a widget. You can do this by calling the `loadInteractionHistory` method on interactive Widget Models. Widgets can have multiple interactions so you can order them by the interaction's `createdAt` property or use the `mostRecentVote` helper property (`mostRecentAnswer` on QuizWidgetModel).

If loading widget models using the `ContentSession().getPostedWidgetModel` method then interaction history will automatically be loaded, you do not have to call `loadInteractionHistory`.
[block:api-header]
{
  "title": "Analytics"
}
[/block]
To improve the accuracy of our built-in analytics and give you stronger insight into how well your Widgets are performing, you should do the following:

1. Call the `registerImpression` method whenever your Widget UI appears on the screen for the User.
2. Call the `markAsInteractive` method whenever your Widget UI becomes interactive for the User. Interactive is loosely defined and depends on your specific implementation and use-case. Typically, the Widget is interactive when user is able to submit votes/answers or open links in the case of Alert Widgets. (Available in version 2.22)