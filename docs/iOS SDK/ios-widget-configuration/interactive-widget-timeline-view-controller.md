---
title: Timeline Widgets
excerpt: iOS guide to Timeline Widgets
deprecated: false
hidden: false
metadata:
  title: iOS Timeline Widgets | LiveLike Developer Hub
  description: >-
    Timeline Widgets are a way to present Widgets in a scrollable list which
    users can browse and interact with past widgets. Learn more.
  robots: index
next:
  description: ''
---
## What are Timeline Widgets?

Timeline Widgets are a way to present Widgets in a scrollable list which user's can browse and interact with past widgets.

You can implement Timeline Widgets into your iOS application using the `InteractiveWidgetTimelineViewController`. It is a UIViewController provided by the EngagementSDK.

## Setup

Create an instance of the InteractiveWidgetTimelineViewController with a ContentSession and apply layout constraints.

```swift
class MyViewController: UIViewController {
  
  private let timelineVC: InteractiveWidgetTimelineViewController
  
  init(contentSession: ContentSession) {
    self.timelineVC = InteractiveWidgetTimelineViewController(contentSession: contentSession)
		super.init(nibName: nil, bundle: nil)
  }
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    // Add timelineVC to layout
    addChild(timelineVC)
		timelineVC.didMove(toParent: self)
    timelineVC.view.translatesAutoresizingMaskIntoConstraints = false     
    view.addSubview(timelineVC.view)
    
    // Apply layout constraints
    NSLayoutConstraint.activate([
    	timelineVC.view.topAnchor.constraint(equalTo: view.topAnchor),
      timelineVC.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
      timelineVC.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
      timelineVC.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
    ])
  }
  
}
```

## Apply Theme

By overriding the makeWidget method of the InteractiveWidgetTimelineViewController you can apply the theme to the stock widgets.

```swift
class MyTimelineViewController: InteractiveWidgetTimelineViewController {
  
  	let myTheme = Theme()
  
    override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {
        let widget = DefaultWidgetFactory.make(from: widgetModel)
        widget?.theme = myTheme
        return widget
    }
}
```

## Using Custom Widget UI

By default, the InteractiveWidgetTimelineViewController will display widgets using the stock Widget UI. If you have built your own Custom Widgets styles it is easy to display those in the *InteractiveWidgetTimelineViewController*.

You will need to make a subclass of *InteractiveWidgetTimelineViewController* and override the `makeWidget` method. In the `makeWidget` method return the `UIViewController` that represents the widget. You can also use `DefaultWidgetFactory` to make an instance of the stock UI that represents the widget.

```swift
class MyTimelineViewController: InteractiveWidgetTimelineViewController {
  
  override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {
    switch widgetModel {
    case .alert(let alertModel):
      // return the UIViewController that represents the widget
    default:
      // you can use the DefaultWidgetFactory to use the stock UI
      return DefaultWidgetFactory.make(from: widgetModel)
    }
  }
  
}
```

## Filtering Widgets

You may want to hide specific widgets types from appearing in the timeline - here is how you can do that:

In this example we will filter all *Alert Widgets* from being displayed in the timeline.

```swift
class MyTimelineViewController: InteractiveWidgetTimelineViewController {
    override func didLoadInitialWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {
      	// filters the alerts from the initial widgets loaded from history
      	return widgetModels.filter { $0.kind != .alert }
    }

    override func didLoadMoreWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {
      	// filters the alerts from the next widgets loaded from history
        return widgetModels.filter { $0.kind != .alert }
    }

    override func didReceiveNewWidget(_ widgetModel: WidgetModel) -> WidgetModel? {
        // filters a new widget if it is an alert
        guard widgetModel.kind != .alert else { return nil }
        return widgetModel
    }
}
```

## Add Custom Spacer between Widgets

By subclassing the InteractiveWidgetTimelineViewController, you can override some UITableViewDelegate methods in order to add a custom view between widgets. The example below adds a view of height 40 and alternates between blue and red for the backgroundColor.

```swift
class MyTimelineViewController: InteractiveWidgetTimelineViewController {

    override func tableView(_ tableView: UITableView, heightForFooterInSection section: Int) -> CGFloat {
        return 40
    }

    override func tableView(_ tableView: UITableView, viewForFooterInSection section: Int) -> UIView? {
        let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: view.frame.width, height: 40))
        if section % 2 != 0 {
            separatorView.backgroundColor = .blue
        } else {
            separatorView.backgroundColor = .red
        }
        return separatorView
    }
}
```
