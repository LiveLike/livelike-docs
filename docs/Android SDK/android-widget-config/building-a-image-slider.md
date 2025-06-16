---
title: Building a Image Slider
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building an Image Slider | Android SDK | LiveLike
  description: >-
    This is a guide on building an Image Slider Widget for Android applications.
    Check out the Image Slider Widget Model to learn more.
  robots: index
next:
  description: ''
---
> 📘 Minimum SDK Version
>
> 2.10

This is a guide on building a custom ImageSlider Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Image Slider Widget Model

The ImageSlider Widget Model is like a ViewModel for ImageSlider Widget.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/imagesliderwidgetmodel/)

***ImageSlider Data(object of LiveLikeWidget class)***\
The ImageSliderr Data provides data about the ImageSlider Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

```kotlin
imageSliderWidgetModel.widgetData.let { widget ->
            widget.options?.get(0)?.imageUrl?.let {
                gauge_seek_bar.setThumbImage(it)
            }
}
```

***Lock in Vote***

For locking your answer to the backend, the widget model contains a method "lockInVote(progress)" which needed progress to send to the backend for locking/submitting the value for the imageSlider.

```kotlin
imageSliderWidgetModel.lockInVote(gauge_seek_bar.getProgress().toDouble())
```

***VoteResults***\
The VoteResults gives you events for updates on the ImageSlider Widget. The event contains the average magnitude changes on the server.

```kotlin
imageSliderWidgetModel.voteResults.subscribe(this) {
            it?.let {
                txt_result.text = "Result: ${it.averageMagnitude}"
            }
        }
```

***Interaction History***\
To load the interaction history, you can call the loadInteractionHistory method\
Eg:

```kotlin
imageSliderWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<EmojiSliderUserInteraction>>(){
            override fun onResponse(result: List<EmojiSliderUserInteraction>?, error: String?) {

            }
        })
```

## Sample Custom Image Slider Widget

```kotlin
class CustomImageSlider : ConstraintLayout {

    lateinit var imageSliderWidgetModel: ImageSliderWidgetModel

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
        inflate(context, R.layout.custom_image_slider, this)
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        imageSliderWidgetModel.widgetData.let { widget ->
            widget.options?.get(0)?.imageUrl?.let {
                gauge_seek_bar.setThumbImage(it)
            }
        }
        gauge_seek_bar.progressChangedCallback = {
            Log.d("Tag","CustomImageSlider Value: $it")
        }
        imageButton4.setOnClickListener {
            imageSliderWidgetModel.lockInVote(gauge_seek_bar.getProgress().toDouble())
            gauge_seek_bar.interactive = false
        }
        imageSliderWidgetModel.voteResults.subscribe(this) {
            it?.let {
                txt_result.text = "Result: ${it.averageMagnitude}"
            }
        }
        imageButton3.setOnClickListener {
            imageSliderWidgetModel.finish()
        }
    }

    override fun onDetachedFromWindow() {
        super.onDetachedFromWindow()
        imageSliderWidgetModel.voteResults.unsubscribe(this)
    }


}
```
