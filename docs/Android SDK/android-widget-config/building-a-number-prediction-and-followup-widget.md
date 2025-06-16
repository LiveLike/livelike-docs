---
title: Building a Number Prediction and followup widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Android Building a Number Prediction & Followup Widget | LiveLike
  description: >-
    This is a guide on building a Number Prediction and Followup Widget for
    Android applications. Learn more.
  robots: index
next:
  description: ''
---
> 📘 Minimum SDK Version

This is a guide on building a custom Number  Prediction and followup Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Number Prediction Widget Model

The Number Prediction Widget Model is responsible for providing prediction specific data and remote apis to submit prediction.

***Number Prediction Data(object of LiveLikeWidget class)***\
The Number Prediction Data provides data about the Number Prediction Widget such as the question and the options consisting of imageUrl and description.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in LiveLikeWidget class for the Number Prediction.\
Example show below:-

```kotlin
widgetData?.let { liveLikeWidget ->
            liveLikeWidget.options?.let { option ->
                if (option.size > 2) {
                    binding.rcylPredictionList.layoutManager =
                        GridLayoutManager(
                            context,
                            2
                        )
                }
                val adapter =
                    PredictionListAdapter(
                        context,
                        isImage,
                        ArrayList(option.map { item -> item!! })
                    )
                binding.rcylPredictionList.adapter = adapter
                  }
                }
```

***lockInVote***\
For submitting the predictions you need to call **lockInVote(options:List<NumberPredictionVotes>)**, with list of NumberPredictionVotes (consisting of the optionId and the number).  It is mandatory to submit the prediction for all the options.

```kotlin
numberPredictionWidgetViewModel?.lockInVote(optionList)
```

***Interaction History***\
To load the interaction history, you can call the loadInteractionHistory method\
Example:-:

```kotlin
numberPredictionWidgetViewModel?.loadInteractionHistory(object :
            LiveLikeCallback<List<NumberPredictionWidgetUserInteraction>>() {
            override fun onResponse(
                result: List<NumberPredictionWidgetUserInteraction>?,
                error: String?
            ) {
                if (!result.isNullOrEmpty()) {
                   // interaction results
                }
            }
        })
```

## Number Prediction FollowUp Widget Model

The follow-up model has the same functions as the above one except lockInVote.

***getPredictionVotes()***\
This method on the model allows you to retrieve the predicted vote list, on which user voted for the prediction associated with this follow up

```kotlin
val votedList = followUpWidgetViewModel?.getPredictionVotes()
```

***claimRewards()***\
    *claims the rewards on the number prediction follow up using a user’s prediction\&#xA;* returns nothing but notifies leaderboard clients

```kotlin
followUpWidgetViewModel?.claimRewards()
```

## Full Number prediction sample with followup

```kotlin
class CustomNumberPredictionWidget :
    ConstraintLayout {
    var numberPredictionWidgetViewModel: NumberPredictionWidgetModel? = null
    var followUpWidgetViewModel: NumberPredictionFollowUpWidgetModel? = null
    private lateinit var binding: CustomNumberPredictionWidgetBinding
    var isImage = false
    var isFollowUp = false

    constructor(context: Context) : super(context) {
        init()
    }

    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {
        init()
    }

    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(
        context,
        attrs,
        defStyle
    ) {
        init()
    }


    private fun init() {
        binding = CustomNumberPredictionWidgetBinding.inflate(
            LayoutInflater.from(context),
            this@CustomNumberPredictionWidget,
            true
        )
    }


    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        var widgetData = numberPredictionWidgetViewModel?.widgetData
        if (isFollowUp) {
            widgetData = followUpWidgetViewModel?.widgetData
        }

        widgetData?.let { liveLikeWidget ->
            liveLikeWidget.options?.let { option ->
                if (option.size > 2) {
                    binding.rcylPredictionList.layoutManager =
                        GridLayoutManager(
                            context,
                            2
                        )
                }

                val adapter =
                    PredictionListAdapter(
                        context,
                        isImage,
                        ArrayList(option.map { item -> item!! })
                    )
                binding.rcylPredictionList.adapter = adapter
                binding.txt.text = liveLikeWidget.question

                getInteractedData(adapter) // get user interaction

                setOnClickListeners(adapter)
                if (isFollowUp) {
                    binding.btn1.visibility = View.GONE
                    claim_rewards.visibility = View.VISIBLE
                } else {
                    binding.btn1.visibility = View.VISIBLE
                    claim_rewards.visibility = View.GONE
                }

                if (isFollowUp) {
                    val votedList = followUpWidgetViewModel?.getPredictionVotes()
                    votedList?.forEach { op ->
                        adapter.predictionMap[op?.optionId!!] = op.number ?: 0
                    }
                    adapter.isFollowUp = true
                } else {
                    result_tv.visibility = GONE
                }
            }

        }
    }

    private fun setOnClickListeners(adapter: PredictionListAdapter) {
        // predict button click
        binding.btn1.setOnClickListener {
            if (!isFollowUp) {
                val optionList = submitVoteRequest(adapter)
                numberPredictionWidgetViewModel?.lockInVote(optionList)
            }
        }
        binding.imgClose.setOnClickListener {
            finish()
        }

        claim_rewards.setOnClickListener{
            followUpWidgetViewModel?.claimRewards()
        }
    }



    private fun submitVoteRequest(adapter: PredictionListAdapter):List<NumberPredictionVotes> {
        val optionList = mutableListOf<NumberPredictionVotes>()
        val maps = adapter.getPredictedScore()
        if(maps.isNullOrEmpty()){
            val options = numberPredictionWidgetViewModel?.widgetData?.options
            for(item in options!!){
                optionList.add(
                    NumberPredictionVotes(
                        optionId = item?.id!!,
                        number = 0
                    )
                )
            }
        }
        return optionList
    }

    //get user interacted data from load history api
    private fun getInteractedData(adapter: PredictionListAdapter) {
        val lists = numberPredictionWidgetViewModel?.getUserInteraction()
        lists?.votes?.let { scores ->
            adapter.setInteractedData(scores)
            adapter.notifyDataSetChanged()
        }
    }

    fun finish() {
        numberPredictionWidgetViewModel?.finish()
        followUpWidgetViewModel?.finish()
    }


    override fun onDetachedFromWindow() {
        super.onDetachedFromWindow()
        // numberPredictionWidgetViewModel?.voteResults?.unsubscribe(this)
    }

      // adapter 
    class PredictionListAdapter(
        private val context: Context,
        private val isImage: Boolean,
        val list: ArrayList<OptionsItem>
    ) : RecyclerView.Adapter<PredictionListAdapter.PredictionListItemViewHolder>() {

        var predictionMap: HashMap<String, Int> = HashMap()
        var isFollowUp = false

        fun getPredictedScore(): HashMap<String, Int> {
            return predictionMap
        }

        class PredictionListItemViewHolder(view: View) : RecyclerView.ViewHolder(view)

        override fun onCreateViewHolder(
            parent: ViewGroup,
            viewType: Int
        ): PredictionListItemViewHolder {
            return PredictionListItemViewHolder(
                LayoutInflater.from(parent.context!!).inflate(
                    R.layout.custom_number_prediction_item,
                    parent, false
                )
            )
        }

        override fun onBindViewHolder(
            holder: PredictionListItemViewHolder,
            position: Int
        ) {
            val item = list[position]

            if (isImage) {
                Glide.with(context)
                    .load(item.imageUrl)
                    .into(
                        holder.itemView.img_1
                    )
                holder.itemView.text_1.visibility = View.GONE
                holder.itemView.img_1.visibility = View.VISIBLE

            } else {
                holder.itemView.text_1.text = item.description
                holder.itemView.text_1.visibility = View.VISIBLE
                holder.itemView.img_1.visibility = View.GONE
            }

            if (isFollowUp) {
                holder.itemView.option_view_1.text = "${predictionMap[item.id!!] ?: 0}"
                holder.itemView.correct_op.text =  item.correctNumber.toString()
                holder.itemView.correct_op.visibility = View.VISIBLE
            }else{
                holder.itemView.correct_op.visibility = View.GONE
            }

            if (!isFollowUp) {
                if (item.number != null) {
                    holder.itemView.option_view_1.text = item.number.toString()
                } else {
                    holder.itemView.option_view_1.text = "0"
                }
            }


            holder.itemView.plus.setOnClickListener {
                if (!isFollowUp) {
                    val updatedScore = holder.itemView.option_view_1.text.toString().toInt() + 1
                    holder.itemView.option_view_1.text = updatedScore.toString()
                    predictionMap[item.id!!] = updatedScore
                }

            }

            holder.itemView.minus.setOnClickListener {
                if (!isFollowUp) {
                    val updatedScore = holder.itemView.option_view_1.text.toString().toInt() - 1
                    holder.itemView.option_view_1.text = updatedScore.toString()
                    predictionMap[item.id!!] = updatedScore
                }
            }
        }


        override fun getItemCount(): Int = list.size

        fun setInteractedData(interactedList: List<NumberPredictionVotes>) {
            for (i in list.indices) {
                if (list[i].id == interactedList[i].optionId) list[i].number =
                    interactedList[i].number
            }
        }
    }
}
```
