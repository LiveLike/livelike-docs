---
title: '[Deprecated] Widget Timeline View Controller'
excerpt: ''
deprecated: true
hidden: false
metadata:
  title: '[Deprecated] Widget Timeline View Controller |  iOS SDK | LiveLike'
  description: >-
    The iOS [Deprecated] WidgetTimelineViewController is a presentation mode
    provided by the Engagement SDK. Learn more.
  robots: index
next:
  description: ''
---
> 🚧 Deprecated!
>
> Version 2.25 introduces the InteractiveWidgetTimelineViewController which is the preferred user experience for a Timeline style presentation mode. We highly recommend using it instead. [https://docs.livelike.com/docs/interactive-widget-timeline-view-controller](https://docs.livelike.com/docs/interactive-widget-timeline-view-controller)

The WidgetTimelineViewController is a presentation mode provided by the EngagementSDK.

Widgets are displayed in a scrollable list view. By default, it displays previously published widget's results and are non-interactive. New widgets received while in Timeline will be interactive for the time set by the producer.

## Setup

```swift
class MyViewController: UIViewController {
  
  private let timelineVC: WidgetTimelineViewController
  
  init(contentSession: ContentSession) {
    self.timelineVC = WidgetTimelineViewController(contentSession: contentSession)
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

## Overriding Default Behaviors

By subclassing the WidgetTimelineViewController you can override some default behaviors to achieve your specific Timeline use-case.  Here are some example use-cases that showcase how to modify the WidgetTimelineViewController's default behaviors:

**Use Case: Custom Widgets**

By default, the WidgetTimelineViewController will display widgets using the Default Widget styles. If you have built your own Custom Widgets styles it is easy to display those in the WidgetTimelineViewController.

```swift
class MyTimelineViewController: WidgetTimelineViewController {
  
  override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {
    switch widgetModel {
      // return the UIViewController that represents the widget
    }
  }
  
}
```

**Use Case: Filtering Widgets**

You may want to hide specific widgets types from appearing in the timeline - here is how you can do that:

In this example we will filter all *Alert Widgets* from being displayed in the timeline.

```swift
class MyTimelineViewController: WidgetTimelineViewController {
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

By subclassing the WidgetTimelineViewController, you can override some UITableViewDelegate methods in order to add a custom view between widgets. The example below adds a view of height 40 and alternates between blue and red for the backgroundColor.

```swift
class MyTimelineViewController: WidgetTimelineViewController {

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