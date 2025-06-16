---
title: Building a Alert Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building an Alert Widget | Android SDK | LiveLike
  description: >-
    This is a guide on building an Alert Widget for Android applications. Check
    out the Alert Widget Model to learn more.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK version",
  "body": "2.8"
}
[/block]
This is a guide on building a custom Alert Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Alert Widget Model"
}
[/block]
***Alert Widget Data***
The Alert Widget Model provides data about the Alert Widget such as the title text, content text, a url to an image and more.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/alertwidgetmodel/)

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.
[block:code]
{
  "codes": [
    {
      "code": "class CustomAlertWidget : ConstraintLayout{\n\n    lateinit var alertModel: AlertWidgetModel\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_alert_widget, this)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        bodyText.text = alertModel.widgetData.title\n        alertModel.widgetData.imageUrl?.let {\n            Glide.with(context)\n                .load(it)\n                .into(bodyImage)\n        }\n    }\n\n\n\n}",
      "language": "kotlin"
    }
  ]
}
[/block]