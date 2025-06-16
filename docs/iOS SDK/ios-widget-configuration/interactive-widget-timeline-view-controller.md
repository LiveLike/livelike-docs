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
[block:api-header]
{
  "title": "What are Timeline Widgets?"
}
[/block]
Timeline Widgets are a way to present Widgets in a scrollable list which user's can browse and interact with past widgets.

You can implement Timeline Widgets into your iOS application using the `InteractiveWidgetTimelineViewController`. It is a UIViewController provided by the EngagementSDK.
[block:api-header]
{
  "title": "Setup"
}
[/block]
Create an instance of the InteractiveWidgetTimelineViewController with a ContentSession and apply layout constraints.
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n  \n  private let timelineVC: InteractiveWidgetTimelineViewController\n  \n  init(contentSession: ContentSession) {\n    self.timelineVC = InteractiveWidgetTimelineViewController(contentSession: contentSession)\n\t\tsuper.init(nibName: nil, bundle: nil)\n  }\n  \n  override func viewDidLoad() {\n    super.viewDidLoad()\n    \n    // Add timelineVC to layout\n    addChild(timelineVC)\n\t\ttimelineVC.didMove(toParent: self)\n    timelineVC.view.translatesAutoresizingMaskIntoConstraints = false     \n    view.addSubview(timelineVC.view)\n    \n    // Apply layout constraints\n    NSLayoutConstraint.activate([\n    \ttimelineVC.view.topAnchor.constraint(equalTo: view.topAnchor),\n      timelineVC.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),\n      timelineVC.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),\n      timelineVC.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)\n    ])\n  }\n  \n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Apply Theme"
}
[/block]
By overriding the makeWidget method of the InteractiveWidgetTimelineViewController you can apply the theme to the stock widgets.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: InteractiveWidgetTimelineViewController {\n  \n  \tlet myTheme = Theme()\n  \n    override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {\n        let widget = DefaultWidgetFactory.make(from: widgetModel)\n        widget?.theme = myTheme\n        return widget\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Using Custom Widget UI"
}
[/block]
By default, the InteractiveWidgetTimelineViewController will display widgets using the stock Widget UI. If you have built your own Custom Widgets styles it is easy to display those in the *InteractiveWidgetTimelineViewController*.

You will need to make a subclass of *InteractiveWidgetTimelineViewController* and override the `makeWidget` method. In the `makeWidget` method return the `UIViewController` that represents the widget. You can also use `DefaultWidgetFactory` to make an instance of the stock UI that represents the widget.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: InteractiveWidgetTimelineViewController {\n  \n  override func makeWidget(_ widgetModel: WidgetModel) -> UIViewController? {\n    switch widgetModel {\n    case .alert(let alertModel):\n      // return the UIViewController that represents the widget\n    default:\n      // you can use the DefaultWidgetFactory to use the stock UI\n      return DefaultWidgetFactory.make(from: widgetModel)\n    }\n  }\n  \n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Filtering Widgets"
}
[/block]
You may want to hide specific widgets types from appearing in the timeline - here is how you can do that:

In this example we will filter all *Alert Widgets* from being displayed in the timeline.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: InteractiveWidgetTimelineViewController {\n    override func didLoadInitialWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {\n      \t// filters the alerts from the initial widgets loaded from history\n      \treturn widgetModels.filter { $0.kind != .alert }\n    }\n\n    override func didLoadMoreWidgets(_ widgetModels: [WidgetModel]) -> [WidgetModel] {\n      \t// filters the alerts from the next widgets loaded from history\n        return widgetModels.filter { $0.kind != .alert }\n    }\n\n    override func didReceiveNewWidget(_ widgetModel: WidgetModel) -> WidgetModel? {\n        // filters a new widget if it is an alert\n        guard widgetModel.kind != .alert else { return nil }\n        return widgetModel\n    }\n}",
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
By subclassing the InteractiveWidgetTimelineViewController, you can override some UITableViewDelegate methods in order to add a custom view between widgets. The example below adds a view of height 40 and alternates between blue and red for the backgroundColor.
[block:code]
{
  "codes": [
    {
      "code": "class MyTimelineViewController: InteractiveWidgetTimelineViewController {\n\n    override func tableView(_ tableView: UITableView, heightForFooterInSection section: Int) -> CGFloat {\n        return 40\n    }\n\n    override func tableView(_ tableView: UITableView, viewForFooterInSection section: Int) -> UIView? {\n        let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: view.frame.width, height: 40))\n        if section % 2 != 0 {\n            separatorView.backgroundColor = .blue\n        } else {\n            separatorView.backgroundColor = .red\n        }\n        return separatorView\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]