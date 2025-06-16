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
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version"
}
[/block]
This is a guide on building a custom Number  Prediction and followup Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Number Prediction Widget Model"
}
[/block]
The Number Prediction Widget Model is responsible for providing prediction specific data and remote apis to submit prediction.

***Number Prediction Data(object of LiveLikeWidget class)***
The Number Prediction Data provides data about the Number Prediction Widget such as the question and the options consisting of imageUrl and description.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in LiveLikeWidget class for the Number Prediction.
Example show below:-
[block:code]
{
  "codes": [
    {
      "code": "widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.options?.let { option ->\n                if (option.size > 2) {\n                    binding.rcylPredictionList.layoutManager =\n                        GridLayoutManager(\n                            context,\n                            2\n                        )\n                }\n                val adapter =\n                    PredictionListAdapter(\n                        context,\n                        isImage,\n                        ArrayList(option.map { item -> item!! })\n                    )\n                binding.rcylPredictionList.adapter = adapter\n                  }\n                }",
      "language": "kotlin"
    }
  ]
}
[/block]
***lockInVote***
For submitting the predictions you need to call **lockInVote(options:List<NumberPredictionVotes>)**, with list of NumberPredictionVotes (consisting of the optionId and the number).  It is mandatory to submit the prediction for all the options.
[block:code]
{
  "codes": [
    {
      "code": " numberPredictionWidgetViewModel?.lockInVote(optionList)",
      "language": "kotlin"
    }
  ]
}
[/block]
***Interaction History***
To load the interaction history, you can call the loadInteractionHistory method
Example:-:

[block:code]
{
  "codes": [
    {
      "code": "  numberPredictionWidgetViewModel?.loadInteractionHistory(object :\n            LiveLikeCallback<List<NumberPredictionWidgetUserInteraction>>() {\n            override fun onResponse(\n                result: List<NumberPredictionWidgetUserInteraction>?,\n                error: String?\n            ) {\n                if (!result.isNullOrEmpty()) {\n                   // interaction results\n                }\n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Number Prediction FollowUp Widget Model"
}
[/block]
The follow-up model has the same functions as the above one except lockInVote.

***getPredictionVotes()***
This method on the model allows you to retrieve the predicted vote list, on which user voted for the prediction associated with this follow up

[block:code]
{
  "codes": [
    {
      "code": " val votedList = followUpWidgetViewModel?.getPredictionVotes()",
      "language": "kotlin"
    }
  ]
}
[/block]
***claimRewards()***
    * claims the rewards on the number prediction follow up using a user’s prediction
    * returns nothing but notifies leaderboard clients
[block:code]
{
  "codes": [
    {
      "code": "followUpWidgetViewModel?.claimRewards()",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Full Number prediction sample with followup"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomNumberPredictionWidget :\n    ConstraintLayout {\n    var numberPredictionWidgetViewModel: NumberPredictionWidgetModel? = null\n    var followUpWidgetViewModel: NumberPredictionFollowUpWidgetModel? = null\n    private lateinit var binding: CustomNumberPredictionWidgetBinding\n    var isImage = false\n    var isFollowUp = false\n\n    constructor(context: Context) : super(context) {\n        init()\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init()\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init()\n    }\n\n\n    private fun init() {\n        binding = CustomNumberPredictionWidgetBinding.inflate(\n            LayoutInflater.from(context),\n            this@CustomNumberPredictionWidget,\n            true\n        )\n    }\n\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        var widgetData = numberPredictionWidgetViewModel?.widgetData\n        if (isFollowUp) {\n            widgetData = followUpWidgetViewModel?.widgetData\n        }\n\n        widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.options?.let { option ->\n                if (option.size > 2) {\n                    binding.rcylPredictionList.layoutManager =\n                        GridLayoutManager(\n                            context,\n                            2\n                        )\n                }\n\n                val adapter =\n                    PredictionListAdapter(\n                        context,\n                        isImage,\n                        ArrayList(option.map { item -> item!! })\n                    )\n                binding.rcylPredictionList.adapter = adapter\n                binding.txt.text = liveLikeWidget.question\n\n                getInteractedData(adapter) // get user interaction\n\n                setOnClickListeners(adapter)\n                if (isFollowUp) {\n                    binding.btn1.visibility = View.GONE\n                    claim_rewards.visibility = View.VISIBLE\n                } else {\n                    binding.btn1.visibility = View.VISIBLE\n                    claim_rewards.visibility = View.GONE\n                }\n\n                if (isFollowUp) {\n                    val votedList = followUpWidgetViewModel?.getPredictionVotes()\n                    votedList?.forEach { op ->\n                        adapter.predictionMap[op?.optionId!!] = op.number ?: 0\n                    }\n                    adapter.isFollowUp = true\n                } else {\n                    result_tv.visibility = GONE\n                }\n            }\n\n        }\n    }\n\n    private fun setOnClickListeners(adapter: PredictionListAdapter) {\n        // predict button click\n        binding.btn1.setOnClickListener {\n            if (!isFollowUp) {\n                val optionList = submitVoteRequest(adapter)\n                numberPredictionWidgetViewModel?.lockInVote(optionList)\n            }\n        }\n        binding.imgClose.setOnClickListener {\n            finish()\n        }\n\n        claim_rewards.setOnClickListener{\n            followUpWidgetViewModel?.claimRewards()\n        }\n    }\n\n\n\n    private fun submitVoteRequest(adapter: PredictionListAdapter):List<NumberPredictionVotes> {\n        val optionList = mutableListOf<NumberPredictionVotes>()\n        val maps = adapter.getPredictedScore()\n        if(maps.isNullOrEmpty()){\n            val options = numberPredictionWidgetViewModel?.widgetData?.options\n            for(item in options!!){\n                optionList.add(\n                    NumberPredictionVotes(\n                        optionId = item?.id!!,\n                        number = 0\n                    )\n                )\n            }\n        }\n        return optionList\n    }\n\n    //get user interacted data from load history api\n    private fun getInteractedData(adapter: PredictionListAdapter) {\n        val lists = numberPredictionWidgetViewModel?.getUserInteraction()\n        lists?.votes?.let { scores ->\n            adapter.setInteractedData(scores)\n            adapter.notifyDataSetChanged()\n        }\n    }\n\n    fun finish() {\n        numberPredictionWidgetViewModel?.finish()\n        followUpWidgetViewModel?.finish()\n    }\n\n\n    override fun onDetachedFromWindow() {\n        super.onDetachedFromWindow()\n        // numberPredictionWidgetViewModel?.voteResults?.unsubscribe(this)\n    }\n\n      // adapter \n    class PredictionListAdapter(\n        private val context: Context,\n        private val isImage: Boolean,\n        val list: ArrayList<OptionsItem>\n    ) : RecyclerView.Adapter<PredictionListAdapter.PredictionListItemViewHolder>() {\n\n        var predictionMap: HashMap<String, Int> = HashMap()\n        var isFollowUp = false\n\n        fun getPredictedScore(): HashMap<String, Int> {\n            return predictionMap\n        }\n\n        class PredictionListItemViewHolder(view: View) : RecyclerView.ViewHolder(view)\n\n        override fun onCreateViewHolder(\n            parent: ViewGroup,\n            viewType: Int\n        ): PredictionListItemViewHolder {\n            return PredictionListItemViewHolder(\n                LayoutInflater.from(parent.context!!).inflate(\n                    R.layout.custom_number_prediction_item,\n                    parent, false\n                )\n            )\n        }\n\n        override fun onBindViewHolder(\n            holder: PredictionListItemViewHolder,\n            position: Int\n        ) {\n            val item = list[position]\n\n            if (isImage) {\n                Glide.with(context)\n                    .load(item.imageUrl)\n                    .into(\n                        holder.itemView.img_1\n                    )\n                holder.itemView.text_1.visibility = View.GONE\n                holder.itemView.img_1.visibility = View.VISIBLE\n\n            } else {\n                holder.itemView.text_1.text = item.description\n                holder.itemView.text_1.visibility = View.VISIBLE\n                holder.itemView.img_1.visibility = View.GONE\n            }\n\n            if (isFollowUp) {\n                holder.itemView.option_view_1.text = \"${predictionMap[item.id!!] ?: 0}\"\n                holder.itemView.correct_op.text =  item.correctNumber.toString()\n                holder.itemView.correct_op.visibility = View.VISIBLE\n            }else{\n                holder.itemView.correct_op.visibility = View.GONE\n            }\n\n            if (!isFollowUp) {\n                if (item.number != null) {\n                    holder.itemView.option_view_1.text = item.number.toString()\n                } else {\n                    holder.itemView.option_view_1.text = \"0\"\n                }\n            }\n\n\n            holder.itemView.plus.setOnClickListener {\n                if (!isFollowUp) {\n                    val updatedScore = holder.itemView.option_view_1.text.toString().toInt() + 1\n                    holder.itemView.option_view_1.text = updatedScore.toString()\n                    predictionMap[item.id!!] = updatedScore\n                }\n\n            }\n\n            holder.itemView.minus.setOnClickListener {\n                if (!isFollowUp) {\n                    val updatedScore = holder.itemView.option_view_1.text.toString().toInt() - 1\n                    holder.itemView.option_view_1.text = updatedScore.toString()\n                    predictionMap[item.id!!] = updatedScore\n                }\n            }\n        }\n\n\n        override fun getItemCount(): Int = list.size\n\n        fun setInteractedData(interactedList: List<NumberPredictionVotes>) {\n            for (i in list.indices) {\n                if (list[i].id == interactedList[i].optionId) list[i].number =\n                    interactedList[i].number\n            }\n        }\n    }\n}",
      "language": "kotlin"
    }
  ]
}
[/block]