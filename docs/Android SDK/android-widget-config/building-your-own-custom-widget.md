---
title: Building Your Own Custom Widget
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This is a guide on using your own Custom Widget UI . Learn more about [Building Custom Widget UI](doc:custom-widget-ui).

[block:api-header]
{
  "title": "Guide"
}
[/block]
**Custom Widget UI in the pop up**

In order to use your own custom widgets over the default one, the integrator can initialize the livelikeWidgetViewFactory variable  [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) of WidgetView class.

Here is an example for the same:
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
Note : For default widget return null

**Custom Widget UI in timeline**

For custom widget [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) implementation has to initialized on timelineview 

Here is an example for the same :
[block:code]
{
  "codes": [
    {
      "code": "timeLineView.widgetViewFactory = TimeLineWidgetFactory(this,timeLineViewModel.timeLineWidgets)",
      "language": "kotlin"
    }
  ]
}
[/block]
You can also mix & match between your custom Widget UI and the stock Widget UI.