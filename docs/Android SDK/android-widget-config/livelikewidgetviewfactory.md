---
title: LiveLikeWidgetViewFactory
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: LiveLikeWidgetViewFactory | Android SDK | LiveLike
  description: >-
    Override your created custom widgets with the default widget by initializing
    the LiveLikeWidgetViewFactory variable of WidgetView class.
  robots: index
next:
  description: ''
---
In order to override your created custom widgets with the default widget, the integrator can initialize the livelikeWidgetViewFactory variable of WidgetView class.
[block:code]
{
  "codes": [
    {
      "code": "widget_view.widgetViewFactory = object : LiveLikeWidgetViewFactory {\n                    override fun createCheerMeterView(viewModel: CheerMeterWidgetmodel): View? {\n                         return CustomCheerMeter(this@ExoPlayerActivity).apply {\n                            cheerMeterWidgetModel = viewModel\n                        }\n                    }\n\n                    override fun createAlertWidgetView(alertWidgetModel: AlertWidgetModel): View? {\n                        return null\n                    }\n                }",
      "language": "kotlin"
    }
  ]
}
[/block]
Note: For default Widget return null

Analytics : Please see [Custom Widget Events](doc:android-analytics#custom-widget-events) for custom widget events