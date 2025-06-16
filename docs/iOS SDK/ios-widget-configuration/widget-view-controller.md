---
title: Popup Widgets
excerpt: iOS guide to Popup Widgets
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The `WidgetPopupViewController` is a presentation controller provided by the EngagementSDK.

It is a pop-up style presenter that displays realtime widgets from the Producer one-at-a-time. The `WidgetPopupViewController` manages a queue of widgets and will automatically show the next widget in the queue after displayed widget is dismissed. 

A swipe to dismiss gesture will be applied to all widgets allowing users to only engage with the widgets they care most about.
[block:api-header]
{
  "title": "Getting Started"
}
[/block]
To setup the `WidgetPopupViewController`, first you need to add it to your layout. This will be the same as adding any `UIViewController` to your layout.

Then, you need set a [ContentSession](https://docs.livelike.com/docs/ios-basic-integration#start-a-content-session) to start displaying real time widgets.
[block:code]
{
  "codes": [
    {
      "code": "class MyViewController: UIViewController {\n  \n  private let widgetVC = WidgetPopupViewController()\n  private let contentSession: ContentSession\n  \n  init(contentSession: ContentSession) {\n    self.contentSession = contentSession\n\t\tsuper.init(nibName: nil, bundle: nil)\n  }\n  \n  override func viewDidLoad() {\n    super.viewDidLoad()\n    \n    // Add widgetVC to layout\n    addChild(widgetVC)\n\t\twidgetVC.didMove(toParent: self)\n    widgetVC.view.translatesAutoresizingMaskIntoConstraints = false     \n    view.addSubview(widgetVC.view)\n    \n    // Apply layout constraints\n    NSLayoutConstraint.activate([\n    \twidgetVC.view.topAnchor.constraint(equalTo: view.topAnchor),\n      widgetVC.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),\n      widgetVC.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),\n      widgetVC.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)\n    ])\n    \n    widgetVC.session = contentSession\n  }\n  \n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Themeing Widgets"
}
[/block]
You can apply a [Theme](doc:custom-themes) to the WidgetPopupViewController to change the styles of the stock widget UI that are displayed.
[block:code]
{
  "codes": [
    {
      "code": "let widgetVC = WidgetPopupViewController()\nlet myTheme = Theme()\nwidgetVC.setTheme(myTheme)",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Using Custom Widgets"
}
[/block]
If you're developing your own [Custom Widget UI](doc:custom-widget-ui), you can easily configure the WidgetPopupViewController to use your custom UI instead of the stock UI. [Read more here](doc:using-custom-widget-ui-with-the-widgetviewcontroller)