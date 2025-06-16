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
> 📘 Minimum SDK Version
>
> 2.11

This is a guide on using your Custom Widget UI with the WidgetPopupViewController. Learn more about [Building Custom Widget UI](doc:custom-widget-ui).

## Guide

The WidgetPopupViewController operates with the `Widget` type. To allow your custom widget to work with the WidgetPopupViewController you must conform to the `Widget` class.

To notify the WidgetPopupViewController to dismiss your custom widget, call the `widgetDidEnterState(widget: WidgetViewModel, state: WidgetState)` method of the `WidgetViewDelegate`.

Here is an example of a custom Alert Widget.

```swift
func MyCustomWidget: Widget {
	
  private let model: AlertWidgetModel
  
  override init(model: AlertWidgetModel) {
  			self.model = model
        super.init(model: model)
  }
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    // Notify widget is finished after 10 seconds 
    DispatchQueue.main.asyncAfter(deadline: .now() + 10) { [weak self] in
      guard let self = self else { return }
      self.delegate?.widgetDidEnterState(widget: self, state: .finished)
    }
  }
}
```

Once your Custom Widget UI is prepared, implement the `willEnqueueWidget` method of the `WidgetPopupViewControllerDelegate`. This is called just before the WidgetPopupViewController is going to display the Widget. Instantiate and return an instance of your Custom Widget UI.

If you only want to override specific widgets you can choose to return the default widget ui by calling the `DefaultWidgetFactory.makeWidget(from:)` function.

Returning `nil` will cause the WidgetPopupViewController to not show a widget.

```swift
func MyViewController: UIViewController {
  
  private let widgetVC: WidgetPopupViewController
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    widgetVC.delegate = self
  }
}

extension MyViewController: WidgetPopupViewControllerDelegate {
  func widgetViewController(
    _ widgetViewController: WidgetPopupViewController, 
   	willEnqueueWidget widgetModel: WidgetModel
  ) -> Widget? {
    switch widgetModel {
    case .alert(let widgetModel):
      // Return our custom ui
      return MyCustomWidget(model: widgetModel)
    default:
      // We will return the default ui for other widgets
      // Since we only want to override the Alert
      return DefaultWidgetFactory.makeWidget(from: widgetModel)
    }
  }
}
```
