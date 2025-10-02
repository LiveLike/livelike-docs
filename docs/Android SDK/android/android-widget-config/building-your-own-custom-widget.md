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

## Guide

**Custom Widget UI in the pop up**

In order to use your own custom widgets over the default one, the integrator can initialize the livelikeWidgetViewFactory variable  [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) of WidgetView class.

Here is an example for the same:

```kotlin
widget_view.widgetViewFactory = object : LiveLikeWidgetViewFactory {
                    override fun createCheerMeterView(viewModel: CheerMeterWidgetmodel): View? {
                         return CustomCheerMeter(this@ExoPlayerActivity).apply {
                            cheerMeterWidgetModel = viewModel
                        }
                    }

                    override fun createAlertWidgetView(alertWidgetModel: AlertWidgetModel): View? {
                        return null
                    }
                }
```

Note : For default widget return null

**Custom Widget UI in timeline**

For custom widget [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) implementation has to initialized on timelineview 

Here is an example for the same :

```kotlin
timeLineView.widgetViewFactory = TimeLineWidgetFactory(this,timeLineViewModel.timeLineWidgets)
```

You can also mix & match between your custom Widget UI and the stock Widget UI.
