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
[block:api-header]
{
  "title": "Linking Sponsor(s) with a Widget"
}
[/block]
When publishing widgets from CMS, producers has to select the sponsors from the list as shown in image below
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c8b70dd-Screenshot_2021-08-09_at_6.03.15_PM.png",
        "Screenshot 2021-08-09 at 6.03.15 PM.png",
        1076,
        961,
        "#222328"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Currently AMA widget is not supported"
}
[/block]

[block:api-header]
{
  "title": "Using Sponsor(s) associated with Widgets"
}
[/block]
If a widget is sent with a sponsor attached, you will see it reflected on the data layer in the widget models. The sample code below demonstrates an Alert widget with a sponsor.
[block:code]
{
  "codes": [
    {
      "code": "guard let widgetModel = widgetModel else { return }\nswitch widgetModel {\n  case .alert(let model):\n  print(\"Widget Model contains \\(model.sponsors.count) Sponsors\")\n  default:\n  print(\"Other widget models\")\n}",
      "language": "swift",
      "name": "iOS"
    },
    {
      "code": "widget_view.widgetViewFactory = object : LiveLikeWidgetViewFactory {\n  override fun createAlertWidgetView(alertWidgetModel: AlertWidgetModel): View? {\n    val sponsors = alertWidgetModel.widgetData.sponsors\n      return SponsoredWidgetView(\n      this@WidgetOnlyActivity,\n      CustomAlertWidget(this@WidgetOnlyActivity).apply {\n        alertModel = alertWidgetModel\n        },\n      alertWidgetModel.widgetData\n    )\n }\n}",
      "language": "kotlin",
      "name": "Android"
    },
    {
      "code": "class CustomAlert extends LiveLikeAlert {\n  render() {\n    return html`\n      <template>\n        <livelike-widget-root>\n          <livelike-widget-header>\n            <livelike-title></livelike-title>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            <span>${this.text}</span>\n            <div>Sponsored By: ${this.widgetPayload.sponsors[0].name}</div>\n          </livelike-widget-body>\n        </livelike-widget-root>\n      <template>\n    `;\n  }\n}\ncustomElements.define(\"custom-alert\", CustomAlert);\n    \nconst widgetContainer = document.querySelector('livelike-widgets');\nwidgetContainer.customWidgetRenderer = ({ widgetPayload }) => {\n  if(widgetPayload.kind === 'alert') {\n    return document.createElement('custom-alert');\n  }\n};",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]