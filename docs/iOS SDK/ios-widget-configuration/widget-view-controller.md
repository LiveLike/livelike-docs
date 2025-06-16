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

## Getting Started

To setup the `WidgetPopupViewController`, first you need to add it to your layout. This will be the same as adding any `UIViewController` to your layout.

Then, you need set a [ContentSession](https://docs.livelike.com/docs/ios-basic-integration#start-a-content-session) to start displaying real time widgets.

```swift
class MyViewController: UIViewController {
  
  private let widgetVC = WidgetPopupViewController()
  private let contentSession: ContentSession
  
  init(contentSession: ContentSession) {
    self.contentSession = contentSession
		super.init(nibName: nil, bundle: nil)
  }
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    // Add widgetVC to layout
    addChild(widgetVC)
		widgetVC.didMove(toParent: self)
    widgetVC.view.translatesAutoresizingMaskIntoConstraints = false     
    view.addSubview(widgetVC.view)
    
    // Apply layout constraints
    NSLayoutConstraint.activate([
    	widgetVC.view.topAnchor.constraint(equalTo: view.topAnchor),
      widgetVC.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
      widgetVC.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
      widgetVC.view.bottomAnchor.constraint(equalTo: view.bottomAnchor)
    ])
    
    widgetVC.session = contentSession
  }
  
}
```

## Themeing Widgets

You can apply a [Theme](doc:custom-themes) to the WidgetPopupViewController to change the styles of the stock widget UI that are displayed.

```swift
let widgetVC = WidgetPopupViewController()
let myTheme = Theme()
widgetVC.setTheme(myTheme)
```

## Using Custom Widgets

If you're developing your own [Custom Widget UI](doc:custom-widget-ui), you can easily configure the WidgetPopupViewController to use your custom UI instead of the stock UI. [Read more here](doc:using-custom-widget-ui-with-the-widgetviewcontroller)
