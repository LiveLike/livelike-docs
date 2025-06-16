---
title: Using Custom Widget UI with the WidgetPopupViewController
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: iOS Using Custom Widget UI With WidgetPopupViewController
  description: >-
    This is a guide on using your iOS Custom Widget UI with the
    WidgetPopupViewController. Learn more.
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
This is a guide on using your Custom Widget UI with the WidgetPopupViewController. Learn more about [Building Custom Widget UI](doc:custom-widget-ui).
[block:api-header]
{
  "title": "Guide"
}
[/block]
The WidgetPopupViewController operates with the `Widget` type. To allow your custom widget to work with the WidgetPopupViewController you must conform to the `Widget` class.

To notify the WidgetPopupViewController to dismiss your custom widget, call the `widgetDidEnterState(widget: WidgetViewModel, state: WidgetState)` method of the `WidgetViewDelegate`.

Here is an example of a custom Alert Widget.
[block:code]
{
  "codes": [
    {
      "code": "func MyCustomWidget: Widget {\n\t\n  private let model: AlertWidgetModel\n  \n  override init(model: AlertWidgetModel) {\n  \t\t\tself.model = model\n        super.init(model: model)\n  }\n  \n  override func viewDidLoad() {\n    super.viewDidLoad()\n    \n    // Notify widget is finished after 10 seconds \n    DispatchQueue.main.asyncAfter(deadline: .now() + 10) { [weak self] in\n      guard let self = self else { return }\n      self.delegate?.widgetDidEnterState(widget: self, state: .finished)\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
Once your Custom Widget UI is prepared, implement the `willEnqueueWidget` method of the `WidgetPopupViewControllerDelegate`. This is called just before the WidgetPopupViewController is going to display the Widget. Instantiate and return an instance of your Custom Widget UI.

If you only want to override specific widgets you can choose to return the default widget ui by calling the `DefaultWidgetFactory.makeWidget(from:)` function.

Returning `nil` will cause the WidgetPopupViewController to not show a widget.
[block:code]
{
  "codes": [
    {
      "code": "func MyViewController: UIViewController {\n  \n  private let widgetVC: WidgetPopupViewController\n  \n  override func viewDidLoad() {\n    super.viewDidLoad()\n    \n    widgetVC.delegate = self\n  }\n}\n\nextension MyViewController: WidgetPopupViewControllerDelegate {\n  func widgetViewController(\n    _ widgetViewController: WidgetPopupViewController, \n   \twillEnqueueWidget widgetModel: WidgetModel\n  ) -> Widget? {\n    switch widgetModel {\n    case .alert(let widgetModel):\n      // Return our custom ui\n      return MyCustomWidget(model: widgetModel)\n    default:\n      // We will return the default ui for other widgets\n      // Since we only want to override the Alert\n      return DefaultWidgetFactory.makeWidget(from: widgetModel)\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]