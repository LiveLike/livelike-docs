---
title: Building a Poll Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building a Poll Widget | Android SDK | LiveLike Developer Hub
  description: >-
    This is a guide on building a Poll Widget for Android applications. Check
    out the Poll Widget Model to learn more.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version",
  "body": "2.9"
}
[/block]
This is a guide on building a custom Poll Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Poll Widget Model"
}
[/block]
The Poll Widget Model is like a ViewModel for Poll Widget.

***Poll Data(object of LiveLikeWidget class)***
The Poll Data provides data about the Poll Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in livelikeWidget class for the poll.

[block:code]
{
  "codes": [
    {
      "code": " pollWidgetModel?.widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.options?.let {\n                if (it.size > 2) {\n                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)\n                }\n                val adapter =\n                    PollListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))\n                rcyl_poll_list.adapter = adapter\n                adapter.pollListener = object : PollListAdapter.PollListener {\n                    override fun onSelectOption(id: String) {\n                        pollWidgetModel?.submitVote(id)\n                    }\n                }\n                button2.visibility = View.GONE\n            }\n        }",
      "language": "kotlin"
    }
  ]
}
[/block]
***SubmitVote***
For submitting or changing the vote on the option for the poll which needed optionId to send to the backend for changing/submitting the vote for the poll.
[block:code]
{
  "codes": [
    {
      "code": "  pollWidgetModel?.submitVote(optionId)",
      "language": "kotlin"
    }
  ]
}
[/block]
***VoteResults***
The VoteResults gives you events for updates on the Poll Widget. The event contains the vote count changes for each option on the server.
[block:code]
{
  "codes": [
    {
      "code": "pollWidgetModel?.voteResults?.subscribe(this) { result ->\n                    result?.choices?.let { options ->\n                        options.forEach { op ->\n                            adapter.optionIdCount[op.id] = op.vote_count ?: 0\n                        }\n                        adapter.notifyDataSetChanged()\n                    }\n                }",
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
      "code": "  pollWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<PollWidgetUserInteraction>>(){\n            override fun onResponse(result: List<PollWidgetUserInteraction>?, error: String?) {\n              \n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sample Custom Poll Widget"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomPollWidget : ConstraintLayout {\n    var pollWidgetModel: PollWidgetModel? = null\n    var isImage = false\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_poll_widget, this@CustomPollWidget)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        pollWidgetModel?.widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.options?.let {\n                if (it.size > 2) {\n                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)\n                }\n                val adapter =\n                    PollListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))\n                rcyl_poll_list.adapter = adapter\n                adapter.pollListener = object : PollListAdapter.PollListener {\n                    override fun onSelectOption(id: String) {\n                        pollWidgetModel?.submitVote(id)\n                    }\n                }\n                button2.visibility = View.GONE\n                pollWidgetModel?.voteResults?.subscribe(this) { result ->\n                    result?.choices?.let { options ->\n                        options.forEach { op ->\n                            adapter.optionIdCount[op.id] = op.vote_count ?: 0\n                        }\n                        adapter.notifyDataSetChanged()\n                    }\n                }\n            }\n            imageView2.setOnClickListener {\n                pollWidgetModel?.finish()\n            }\n\n        }\n\n    }\n\n    override fun onDetachedFromWindow() {\n        super.onDetachedFromWindow()\n        pollWidgetModel?.voteResults?.unsubscribe(this)\n    }\n}\n\nclass PollListAdapter(\n    private val context: Context,\n    private val isImage: Boolean,\n    val list: ArrayList<OptionsItem>\n) :\n    RecyclerView.Adapter<PollListAdapter.PollListItemViewHolder>() {\n    private var selectedIndex = -1\n    val optionIdCount: HashMap<String, Int> = hashMapOf()\n    fun getSelectedOption(): OptionsItem? = when (selectedIndex > -1) {\n        true -> list[selectedIndex]\n        else -> null\n    }\n\n    var pollListener: PollListener? = null\n\n    interface PollListener {\n        fun onSelectOption(id: String)\n    }\n\n    class PollListItemViewHolder(view: View) : RecyclerView.ViewHolder(view)\n\n    override fun onCreateViewHolder(p0: ViewGroup, p1: Int): PollListItemViewHolder {\n        return PollListItemViewHolder(\n            LayoutInflater.from(p0.context!!).inflate(\n                when (isImage) {\n                    true -> R.layout.quiz_image_list_item\n                    else -> R.layout.quiz_list_item\n                }, p0, false\n            )\n        )\n    }\n\n    override fun onBindViewHolder(holder: PollListItemViewHolder, index: Int) {\n        val item = list[index]\n        if (isImage) {\n            Glide.with(context)\n                .load(item.imageUrl)\n                .into(holder.itemView.imageButton2)\n            if (selectedIndex == index) {\n                holder.itemView.imageButton2.setBackgroundColor(Color.BLUE)\n            } else {\n                holder.itemView.imageButton2.setBackgroundColor(Color.GRAY)\n            }\n            holder.itemView.textView8.text = \"${optionIdCount[item.id!!] ?: 0}\"\n\n            holder.itemView.imageButton2.setOnClickListener {\n                selectedIndex = holder.adapterPosition\n                pollListener?.onSelectOption(item.id!!)\n                notifyDataSetChanged()\n            }\n        } else {\n            holder.itemView.textView7.text = \"${optionIdCount[item.id!!] ?: 0}\"\n            holder.itemView.button4.text = \"${item.description}\"\n            if (selectedIndex == index) {\n                holder.itemView.button4.setBackgroundColor(Color.BLUE)\n            } else {\n                holder.itemView.button4.setBackgroundColor(Color.GRAY)\n            }\n\n            holder.itemView.button4.setOnClickListener {\n                selectedIndex = holder.adapterPosition\n                pollListener?.onSelectOption(item.id!!)\n                notifyDataSetChanged()\n            }\n        }\n\n    }\n\n    override fun getItemCount(): Int = list.size\n}\n",
      "language": "kotlin"
    }
  ]
}
[/block]