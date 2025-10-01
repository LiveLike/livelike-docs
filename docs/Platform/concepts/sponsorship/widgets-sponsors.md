---
title: Widgets Sponsors
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Sponsors | LiveLike Developer Hub
  description: >-
    When publishing widgets from the CMS, producers have to select the sponsors
    from a provided list. Learn more about widget sponsors.
  robots: index
next:
  description: ''
---
## Linking Sponsor(s) with a Widget

When publishing widgets from CMS, producers has to select the sponsors from the list as shown in image below

![1076](https://files.readme.io/c8b70dd-Screenshot_2021-08-09_at_6.03.15_PM.png "Screenshot 2021-08-09 at 6.03.15 PM.png")

> 📘 Currently AMA widget is not supported

## Using Sponsor(s) associated with Widgets

If a widget is sent with a sponsor attached, you will see it reflected on the data layer in the widget models. The sample code below demonstrates an Alert widget with a sponsor.

```swift iOS
guard let widgetModel = widgetModel else { return }
switch widgetModel {
  case .alert(let model):
  print("Widget Model contains \(model.sponsors.count) Sponsors")
  default:
  print("Other widget models")
}
```
```kotlin Android
widget_view.widgetViewFactory = object : LiveLikeWidgetViewFactory {
  override fun createAlertWidgetView(alertWidgetModel: AlertWidgetModel): View? {
    val sponsors = alertWidgetModel.widgetData.sponsors
      return SponsoredWidgetView(
      this@WidgetOnlyActivity,
      CustomAlertWidget(this@WidgetOnlyActivity).apply {
        alertModel = alertWidgetModel
        },
      alertWidgetModel.widgetData
    )
 }
}
```
```javascript JavaScript
class CustomAlert extends LiveLikeAlert {
  render() {
    return html`
      <template>
        <livelike-widget-root>
          <livelike-widget-header>
            <livelike-title></livelike-title>
          </livelike-widget-header>
          <livelike-widget-body>
            <span>${this.text}</span>
            <div>Sponsored By: ${this.widgetPayload.sponsors[0].name}</div>
          </livelike-widget-body>
        </livelike-widget-root>
      <template>
    `;
  }
}
customElements.define("custom-alert", CustomAlert);
    
const widgetContainer = document.querySelector('livelike-widgets');
widgetContainer.customWidgetRenderer = ({ widgetPayload }) => {
  if(widgetPayload.kind === 'alert') {
    return document.createElement('custom-alert');
  }
};
```
