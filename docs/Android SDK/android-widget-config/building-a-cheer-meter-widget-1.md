---
title: Building a Cheer Meter Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
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
This is a guide on building a custom Cheer Meter Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Cheer Meter Widget Model"
}
[/block]
The Cheer Meter Widget Model is like a ViewModel for Cheer Meter Widget.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/cheermeterwidgetmodel/)

***Cheer Meter Data(object of LiveLikeWidget class)***
The Cheer Meter Data provides data about the Cheer Meter such as the title text and the Cheer Meter options. The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.
[block:code]
{
  "codes": [
    {
      "code": " override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        \n        cheerMeterWidgetModel?.widgetData?.let { livelikeWidget ->\n\t\t\t\t// get data for cheermeter\n          Glide.with(context)\n                .load(livelikeWidget.options?.get(0)?.imageUrl)\n                .into(btn_1)\n\n            Glide.with(context)\n                .load(livelikeWidget.options?.get(1)?.imageUrl)\n                .into(btn_2)\n\n        }\n    }",
      "language": "kotlin"
    }
  ]
}
[/block]
***Submit a vote***
Due to the high volume of votes expected on a Cheer Meter, the SDK will batch the votes puts a 1-second throttle on the vote request or until reaching the threshold value.To submit a vote take the id of the option and call `submitVote(optionID:)`
[block:code]
{
  "codes": [
    {
      "code": "\t\t\t\t\t\t btn_1.setOnClickListener {\n               cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(0)?.id!!)\n            }\n            btn_2.setOnClickListener {\n             cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(1)?.id!!)\n            }",
      "language": "kotlin"
    }
  ]
}
[/block]
***VoteResults***
The VoteResults gives you events for updates on the Cheer Meter. The event contains the vote count changes on the server.
[block:code]
{
  "codes": [
    {
      "code": " override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        cheerMeterWidgetModel?.voteResults?.subscribe(this.javaClass) {\n            //get updated vote count\n           \tval op1 = it?.choices?.get(0)\n            val op2 = it?.choices?.get(1)\n            val vt1 = op1?.vote_count ?: 0\n            val vt2 = op2?.vote_count ?: 0\n            val total = vt1 + vt2\n            if (total > 0) {\n                val perVt1 = (vt1.toFloat() / total.toFloat()) * 100\n                val perVt2 = (vt2.toFloat() / total.toFloat()) * 100\n                speed_view_1.setSpeedAt(perVt1)\n                speed_view_2.setSpeedAt(perVt2)\n                txt_team1.text = \"$perVt1\"\n                txt_team2.text = \"$perVt2\"\n            }\n        }\n } ",
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
      "code": "  cheerMeterWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<CheerMeterUserInteraction>>(){\n            override fun onResponse(result: List<CheerMeterUserInteraction>?, error: String?) {\n              \n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sample Custom Cheer Meter"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomCheerMeter : ConstraintLayout {\n\n    private lateinit var mCountDownTimer: CountDownTimer\n    var cheerMeterWidgetModel: CheerMeterWidgetmodel? = null\n\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_cheer_meter, this@CustomCheerMeter)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        cheerMeterWidgetModel?.voteResults?.subscribe(this.javaClass) {\n            //get updated vote count\n           \tval op1 = it?.choices?.get(0)\n            val op2 = it?.choices?.get(1)\n            val vt1 = op1?.vote_count ?: 0\n            val vt2 = op2?.vote_count ?: 0\n            val total = vt1 + vt2\n            if (total > 0) {\n                val perVt1 = (vt1.toFloat() / total.toFloat()) * 100\n                val perVt2 = (vt2.toFloat() / total.toFloat()) * 100\n                speed_view_1.setSpeedAt(perVt1)\n                speed_view_2.setSpeedAt(perVt2)\n                txt_team1.text = \"$perVt1\"\n                txt_team2.text = \"$perVt2\"\n            }\n        }\n\n        cheerMeterWidgetModel?.widgetData?.let { livelikeWidget ->\n\t\t\t\t// get data for cheermeter\n          Glide.with(context)\n                .load(livelikeWidget.options?.get(0)?.imageUrl)\n                .into(btn_1)\n\n            Glide.with(context)\n                .load(livelikeWidget.options?.get(1)?.imageUrl)\n                .into(btn_2)\n\t\t\t\t\t btn_1.setOnClickListener {\n            cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(0)?.id!!)\n           }\n           btn_2.setOnClickListener {\n        \t\tcheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(1)?.id!!)\n           }\n            val handler = Handler()\n            handler.postDelayed({\n                cheerMeterWidgetModel?.finish()\n                mCountDownTimer.onFinish()\n            }, parseDuration(livelikeWidget.timeout ?: \"\"))\n\n            var i = 0\n            val timer = parseDuration(livelikeWidget.timeout ?: \"\")\n            mCountDownTimer = object : CountDownTimer(timer, 1000) {\n                override fun onTick(millisUntilFinished: Long) {\n                    i++\n                    progress_bar.progress = (i * 100 / (timer / 1000)).toInt()\n                }\n\n                override fun onFinish() {\n                    //Do what you want\n                    i++\n                    progress_bar.progress = 100\n                }\n            }\n            mCountDownTimer.start()\n        }\n    }\n\t\t\n    override fun onDetachedFromWindow() {\n        super.onDetachedFromWindow()\n        //Unsubscribe from the voteResult events \n        cheerMeterWidgetModel?.voteResults?.unsubscribe(this.javaClass)\n    }\n}\n",
      "language": "kotlin"
    }
  ]
}
[/block]