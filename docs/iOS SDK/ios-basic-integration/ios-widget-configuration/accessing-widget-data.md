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
> 📘 Minimum SDK Version
>
> 2.11

This is an iOS guide on Widget Models as part of the Custom Widget UI system. For an overview on Custom Widget UI see [Building Custom Widget UI](doc:custom-widget-ui).

## What are Widget Models?

Widget Models are representations of a Widget as it is on the server. Widget Models give you the access to read a Widget's data, submit votes, and observe changes to the Widget. Ultimately, a Widget Model provides everything for you to build Custom UI to support your use case. 

While each Widget has a unique Widget Model class that represents it, they are encapsulated under the WidgetModel enum *TODO LINK* in order to simplify the access methods. Use a `switch` statement on WidgetModel to get the exact Widget Model.

There are 3 ways to access/retrieve a Widget Model to support various use-cases. All 3 methods require a ContentSession. For more information on Content Session see [Getting Started](doc:ios-basic-integration). 

## Subscribing to Realtime Widget Models

Implement the ContentSessionDelegate to observe when a Widget is published by the Producer.

```swift
class MyViewController: UIViewController {
    
  let session: ContentSession
    
  override func viewDidLoad() {
    super.viewDidLoad()
      
    session.delegate = self
  }
}

extension MyViewController: ContentSessionDelegate {
  func contentSession(_ session: ContentSession, didReceiveWidget widgetModel: WidgetModel) {
    switch widgetModel {
     	// Do something with widgetModel
    }
  }
}
```

## Get a Widget Model by ID

If you know the widget id and kind you can choose to fetch the widget model from the server.

```swift
class MyViewController: UIViewController {
    
  let session: ContentSession
  let widgetID: String
  let widgetKind: WidgetKind
    
  override func viewDidLoad() {
  	super.viewDidLoad()
        
    session.getWidgetModel(id: widgetID, kind: widgetKind) { result in
   	  switch result {
      case .success(let widgetModel):
  	  	switch widgetModel {
      	  // Do something with widgetModel
      	}
      case .failure(let error):
      	// handle error
      }
    }
  }
}
```

> ❗️ `getWidgetModels()`
>
> The `getWidgetModels()` SDK interface will be available in iOS SDK version 2.37

## Getting Widget Models

This method can be used to fetch a paginated result of Widgets Models filtered by the `options` parameter.\
The request filters and sorts are defined in the `GetWidgetsRequestOptions` struct. 

The filtering options include:

* widgetKind - The set of widget kinds to include
* widgetStatus - The publishing status of the widget
* widgetOrdering - The order in which the widgets will be returned
* interactive - Filters for only widgets that can still be interacted with
* since - A Date parameter that filters out widgets with an earlier created date

```swift
class MyViewController: UIViewController {
    
  let session: ContentSession
    
  override func viewDidLoad() {
  	super.viewDidLoad()
    
    let options = GetWidgetModelsRequestOptions(
      widgetStatus: .published,
      widgetKind: [.textPoll, .imagePrediction],
      widgetOrdering: .recent
    )
    
    session.getWidgetModels(
      page: .first,
      options: options
    ) { result in
       switch result {
         case let .success(widgets):
         case let .failure(error):
       }
      }    
  }
}
```

## Get Published Widget Models from History

For use-cases like a Timeline mode, you can perform a paginated fetch of the most recent widget models (\~20) on the server. Call with `.first` to get the first page then you may call using `.next` for subsequent pages.

```swift
class MyViewController: UIViewController {
    
  let session: ContentSession
   
  override func viewDidLoad() {
    super.viewDidLoad()        
        
    session.getPostedWidgetModel(page: .first) { result in
      switch result {
      case .success(let widgetModels):
      	switch widgetModel {
      	  // Do something with widgetModel
      	}
     	case .failure(let error):
        // handle error
      }
    }
  }
}
```

## Interaction History

*Available in version 2.24*

For many use-cases you may be interested in loading the user's interaction history on a widget. You can do this by calling the `loadInteractionHistory` method on interactive Widget Models. Widgets can have multiple interactions so you can order them by the interaction's `createdAt` property or use the `mostRecentVote` helper property (`mostRecentAnswer` on QuizWidgetModel).

If loading widget models using the `ContentSession().getPostedWidgetModel` method then interaction history will automatically be loaded, you do not have to call `loadInteractionHistory`.

## Analytics

To improve the accuracy of our built-in analytics and give you stronger insight into how well your Widgets are performing, you should do the following:

1. Call the `registerImpression` method whenever your Widget UI appears on the screen for the User.
2. Call the `markAsInteractive` method whenever your Widget UI becomes interactive for the User. Interactive is loosely defined and depends on your specific implementation and use-case. Typically, the Widget is interactive when user is able to submit votes/answers or open links in the case of Alert Widgets. (Available in version 2.22)
