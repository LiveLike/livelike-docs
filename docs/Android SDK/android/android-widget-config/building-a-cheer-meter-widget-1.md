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
> 📘 Minimum SDK version
>
> 2.8

This is a guide on building a custom Cheer Meter Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Cheer Meter Widget Model

The Cheer Meter Widget Model is like a ViewModel for Cheer Meter Widget.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/cheermeterwidgetmodel/)

***Cheer Meter Data(object of LiveLikeWidget class)***\
The Cheer Meter Data provides data about the Cheer Meter such as the title text and the Cheer Meter options. The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

```kotlin
override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        
        cheerMeterWidgetModel?.widgetData?.let { livelikeWidget ->
				// get data for cheermeter
          Glide.with(context)
                .load(livelikeWidget.options?.get(0)?.imageUrl)
                .into(btn_1)

            Glide.with(context)
                .load(livelikeWidget.options?.get(1)?.imageUrl)
                .into(btn_2)

        }
    }
```

***Submit a vote***\
Due to the high volume of votes expected on a Cheer Meter, the SDK will batch the votes puts a 1-second throttle on the vote request or until reaching the threshold value.To submit a vote take the id of the option and call `submitVote(optionID:)`

```kotlin
btn_1.setOnClickListener {
               cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(0)?.id!!)
            }
            btn_2.setOnClickListener {
             cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(1)?.id!!)
            }
```

***VoteResults***\
The VoteResults gives you events for updates on the Cheer Meter. The event contains the vote count changes on the server.

```kotlin
override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        cheerMeterWidgetModel?.voteResults?.subscribe(this.javaClass) {
            //get updated vote count
           	val op1 = it?.choices?.get(0)
            val op2 = it?.choices?.get(1)
            val vt1 = op1?.vote_count ?: 0
            val vt2 = op2?.vote_count ?: 0
            val total = vt1 + vt2
            if (total > 0) {
                val perVt1 = (vt1.toFloat() / total.toFloat()) * 100
                val perVt2 = (vt2.toFloat() / total.toFloat()) * 100
                speed_view_1.setSpeedAt(perVt1)
                speed_view_2.setSpeedAt(perVt2)
                txt_team1.text = "$perVt1"
                txt_team2.text = "$perVt2"
            }
        }
 }
```

***Interaction History***\
To load the interaction history, you can call the loadInteractionHistory method\
Eg:

```kotlin
cheerMeterWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<CheerMeterUserInteraction>>(){
            override fun onResponse(result: List<CheerMeterUserInteraction>?, error: String?) {
              
            }
        })
```

## Sample Custom Cheer Meter

```kotlin
class CustomCheerMeter : ConstraintLayout {

    private lateinit var mCountDownTimer: CountDownTimer
    var cheerMeterWidgetModel: CheerMeterWidgetmodel? = null


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
        inflate(context, R.layout.custom_cheer_meter, this@CustomCheerMeter)
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        cheerMeterWidgetModel?.voteResults?.subscribe(this.javaClass) {
            //get updated vote count
           	val op1 = it?.choices?.get(0)
            val op2 = it?.choices?.get(1)
            val vt1 = op1?.vote_count ?: 0
            val vt2 = op2?.vote_count ?: 0
            val total = vt1 + vt2
            if (total > 0) {
                val perVt1 = (vt1.toFloat() / total.toFloat()) * 100
                val perVt2 = (vt2.toFloat() / total.toFloat()) * 100
                speed_view_1.setSpeedAt(perVt1)
                speed_view_2.setSpeedAt(perVt2)
                txt_team1.text = "$perVt1"
                txt_team2.text = "$perVt2"
            }
        }

        cheerMeterWidgetModel?.widgetData?.let { livelikeWidget ->
				// get data for cheermeter
          Glide.with(context)
                .load(livelikeWidget.options?.get(0)?.imageUrl)
                .into(btn_1)

            Glide.with(context)
                .load(livelikeWidget.options?.get(1)?.imageUrl)
                .into(btn_2)
					 btn_1.setOnClickListener {
            cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(0)?.id!!)
           }
           btn_2.setOnClickListener {
        		cheerMeterWidgetModel?.submitVote(livelikeWidget.options?.get(1)?.id!!)
           }
            val handler = Handler()
            handler.postDelayed({
                cheerMeterWidgetModel?.finish()
                mCountDownTimer.onFinish()
            }, parseDuration(livelikeWidget.timeout ?: ""))

            var i = 0
            val timer = parseDuration(livelikeWidget.timeout ?: "")
            mCountDownTimer = object : CountDownTimer(timer, 1000) {
                override fun onTick(millisUntilFinished: Long) {
                    i++
                    progress_bar.progress = (i * 100 / (timer / 1000)).toInt()
                }

                override fun onFinish() {
                    //Do what you want
                    i++
                    progress_bar.progress = 100
                }
            }
            mCountDownTimer.start()
        }
    }
		
    override fun onDetachedFromWindow() {
        super.onDetachedFromWindow()
        //Unsubscribe from the voteResult events 
        cheerMeterWidgetModel?.voteResults?.unsubscribe(this.javaClass)
    }
}
```
