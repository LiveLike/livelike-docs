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
> 📘 Minimum SDK version
>
> 2.8

This is a guide on building a custom Alert Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Alert Widget Model

***Alert Widget Data***\
The Alert Widget Model provides data about the Alert Widget such as the title text, content text, a url to an image and more.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/alertwidgetmodel/)

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

```kotlin
class CustomAlertWidget : ConstraintLayout{

    lateinit var alertModel: AlertWidgetModel

    constructor(context: Context) : super(context) {
        init(null, 0)
    }

    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {
        init(attrs, 0)
    }

    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(
        context,
        attrs,
        defStyle
    ) {
        init(attrs, defStyle)
    }

    private fun init(attrs: AttributeSet?, defStyle: Int) {
        inflate(context, R.layout.custom_alert_widget, this)
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        bodyText.text = alertModel.widgetData.title
        alertModel.widgetData.imageUrl?.let {
            Glide.with(context)
                .load(it)
                .into(bodyImage)
        }
    }



}
```
