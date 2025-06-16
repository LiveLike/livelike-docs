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
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version",
  "body": "2.10"
}
[/block]
This is a guide on building a custom ImageSlider Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Image Slider Widget Model"
}
[/block]
The ImageSlider Widget Model is like a ViewModel for ImageSlider Widget.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/imagesliderwidgetmodel/)

***ImageSlider Data(object of LiveLikeWidget class)***
The ImageSliderr Data provides data about the ImageSlider Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

[block:code]
{
  "codes": [
    {
      "code": "imageSliderWidgetModel.widgetData.let { widget ->\n            widget.options?.get(0)?.imageUrl?.let {\n                gauge_seek_bar.setThumbImage(it)\n            }\n}",
      "language": "kotlin"
    }
  ]
}
[/block]
***Lock in Vote***

For locking your answer to the backend, the widget model contains a method "lockInVote(progress)" which needed progress to send to the backend for locking/submitting the value for the imageSlider.


[block:code]
{
  "codes": [
    {
      "code": "imageSliderWidgetModel.lockInVote(gauge_seek_bar.getProgress().toDouble())",
      "language": "kotlin"
    }
  ]
}
[/block]
***VoteResults***
The VoteResults gives you events for updates on the ImageSlider Widget. The event contains the average magnitude changes on the server.
[block:code]
{
  "codes": [
    {
      "code": " imageSliderWidgetModel.voteResults.subscribe(this) {\n            it?.let {\n                txt_result.text = \"Result: ${it.averageMagnitude}\"\n            }\n        }",
      "language": "kotlin"
    }
  ]
}
[/block]
***Interaction History***
To load the interaction history, you can call the loadInteractionHistory method
Eg:
[block:code]
{
  "codes": [
    {
      "code": "  imageSliderWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<EmojiSliderUserInteraction>>(){\n            override fun onResponse(result: List<EmojiSliderUserInteraction>?, error: String?) {\n\n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sample Custom Image Slider Widget"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomImageSlider : ConstraintLayout {\n\n    lateinit var imageSliderWidgetModel: ImageSliderWidgetModel\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_image_slider, this)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        imageSliderWidgetModel.widgetData.let { widget ->\n            widget.options?.get(0)?.imageUrl?.let {\n                gauge_seek_bar.setThumbImage(it)\n            }\n        }\n        gauge_seek_bar.progressChangedCallback = {\n            Log.d(\"Tag\",\"CustomImageSlider Value: $it\")\n        }\n        imageButton4.setOnClickListener {\n            imageSliderWidgetModel.lockInVote(gauge_seek_bar.getProgress().toDouble())\n            gauge_seek_bar.interactive = false\n        }\n        imageSliderWidgetModel.voteResults.subscribe(this) {\n            it?.let {\n                txt_result.text = \"Result: ${it.averageMagnitude}\"\n            }\n        }\n        imageButton3.setOnClickListener {\n            imageSliderWidgetModel.finish()\n        }\n    }\n\n    override fun onDetachedFromWindow() {\n        super.onDetachedFromWindow()\n        imageSliderWidgetModel.voteResults.unsubscribe(this)\n    }\n\n\n}",
      "language": "kotlin"
    }
  ]
}
[/block]