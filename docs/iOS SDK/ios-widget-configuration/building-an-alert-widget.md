---
title: Building an Alert Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building an Alert Widget | iOS SDK | LiveLike Developer Hub
  description: >-
    This is a guide on building an Alert Widget. Check out the Alert Widget
    Model to learn more.
  robots: index
next:
  description: ''
---
> 📘 Minimum SDK Version
>
> 2.11

This is a guide on building a custom Alert Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

> 📘 Considerations for WidgetPopupViewController
>
> If you plan on using your Custom Widget UI with the WidgetPopupViewController see [Using Custom Widget UI with the WidgetPopupViewController](doc:using-custom-widget-ui-with-the-widgetviewcontroller)

## AlertWidgetModel

[API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/AlertWidgetModel.html)

***Alert Widget Data***\
The Alert Widget Model provides data about the Alert Widget such as the title text, content text, a url to an image and more.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

***Open Link URL***\
An Alert Widget has the ability to include a link to a url. To open the link included in the Alert Widget, you can use the `openLinkUrl()` method. 

```swift Swift
func CustomAlertWidget: UIViewController {
  
  private let model: AlertWidgetModel
  
  init(model: AlertWidgetModel) {
    self.model = model
    super.init(nibName: nil, bundle: nil)
  }
  
  // Opening the Alert Widget link
  // <UIButton>.addTarget(self, action: #selector(showLink), for: .touchUpInside) 
  @objc func showLink() {
    viewModel.openLinkUrl()
  }
}
```
