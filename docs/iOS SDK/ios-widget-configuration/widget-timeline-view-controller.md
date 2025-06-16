---
title: '[Deprecated] Widget Timeline View Controller'
excerpt: ''
deprecated: false
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
[block:callout]
{
  "type": "warning",
  "title": "Deprecated!",
  "body": "Version 2.25 introduces the InteractiveWidgetTimelineViewController which is the preferred user experience for a Timeline style presentation mode. We highly recommend using it instead. https://docs.livelike.com/docs/interactive-widget-timeline-view-controller"
}
[/block]
The WidgetTimelineViewController is a presentation mode provided by the EngagementSDK.

Widgets are displayed in a scrollable list view. By default, it displays previously published widget's results and are non-interactive. New widgets received while in Timeline will be interactive for the time set by the producer.
[block:api-header]
{
  "title": "Setup"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n  \n  private let timelineVC: WidgetTimelineViewController\n  \n  init(contentSession: ContentSession) {\n    self.timelineVC = WidgetTimelineViewController(contentSession: contentSession)\n\t\tsuper.init(nibName: nil, bundle: nil)\n  }\n  \n  override func viewDidLoad() {\n    super.viewDidLoad()\n    \n    // Add timelineVC to layout\n    addChild(timelineVC)\n\t\ttimelineVC.didMove(toParent: self)\n    timelineVC.view.translatesAutoresizingMaskIntoConstraints = false     \n    view.addSubview(timelineVC.view)\n    \n    // Apply layout constraints\n    NSLayoutConstraint.activate([\n    \ttimelineVC.view.topAnchor.constraint(equalTo: view.topAnchor),\n      timelineVC.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),\n      timelineVC.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),\n      timelineVC.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)\n    ])\n  }\n  \n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Overriding Default Behaviors"
}
[/block]
By subclassing the WidgetTimelineViewController you can override some default behaviors to achieve your specific Timeline use-case.  Here are some example use-cases that showcase how to modify the WidgetTimelineViewController's default behaviors:

**Use Case: Custom Widgets**

By default, the WidgetTimelineViewController will display widgets using the Default Widget styles. If you have built your own Custom Widgets styles it is easy to display those in the WidgetTimelineViewController.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: WidgetTimelineViewController {\n  \n  override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {\n    switch widgetModel {\n      // return the UIViewController that represents the widget\n    }\n  }\n  \n}",
      "language": "swift"
    }
  ]
}
[/block]
**Use Case: Filtering Widgets**

You may want to hide specific widgets types from appearing in the timeline - here is how you can do that:

In this example we will filter all *Alert Widgets* from being displayed in the timeline.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: WidgetTimelineViewController {\n    override func didLoadInitialWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {\n      \t// filters the alerts from the initial widgets loaded from history\n      \treturn widgetModels.filter { $0.kind != .alert }\n    }\n\n    override func didLoadMoreWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {\n      \t// filters the alerts from the next widgets loaded from history\n        return widgetModels.filter { $0.kind != .alert }\n    }\n\n    override func didReceiveNewWidget(_ widgetModel: WidgetModel) -> WidgetModel? {\n        // filters a new widget if it is an alert\n        guard widgetModel.kind != .alert else { return nil }\n        return widgetModel\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Add Custom Spacer between Widgets"
}
[/block]
By subclassing the WidgetTimelineViewController, you can override some UITableViewDelegate methods in order to add a custom view between widgets. The example below adds a view of height 40 and alternates between blue and red for the backgroundColor.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: WidgetTimelineViewController {\n\n    override func tableView(_ tableView: UITableView, heightForFooterInSection section: Int) -> CGFloat {\n        return 40\n    }\n\n    override func tableView(_ tableView: UITableView, viewForFooterInSection section: Int) -> UIView? {\n        let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: view.frame.width, height: 40))\n        if section % 2 != 0 {\n            separatorView.backgroundColor = .blue\n        } else {\n            separatorView.backgroundColor = .red\n        }\n        return separatorView\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]