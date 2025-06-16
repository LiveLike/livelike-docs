---
title: Building a Quiz Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building a Quiz Widget | Android SDK | LiveLike
  description: >-
    This is a guide on building a Quiz Widget for Android applications. Check
    out the Alert Widget Model to learn more.
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
This is a guide on building a custom Quiz Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Quiz Widget Model"
}
[/block]
The Quiz Widget Model is like a ViewModel for Quiz Widget.

[API Reference](https://livelike.github.io/engagement-sdk-android-docs/kotlindoc/com/livelike/engagementsdk/widget/widgetmodel/quizwidgetmodel/)

***Quiz Data(object of LiveLikeWidget class)***
The Quiz Data provides data about the Quiz Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

[block:code]
{
  "codes": [
    {
      "code": " quizWidgetModel?.widgetData?.let { liveLikeWidget ->\n            title.text=\"${liveLikeWidget.question}\"\n            liveLikeWidget.choices?.let {\n                val adapter =\n                    QuizListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))\n                rcyl_quiz_list.adapter = adapter\n   \t\t\t\t\t}\n }                                   ",
      "language": "kotlin"
    }
  ]
}
[/block]
***Lock in Answer***

For locking your answer to the backend, the widget model contains a method "lockInAnswer(optionId)" which needed option id to send to the backend for locking/submitting the answer for the quiz.

Note: Once the answer is locked in the backend it cannot be changed/update and for that quiz,also no other option will be accepted by the backend.


[block:code]
{
  "codes": [
    {
      "code": "quizWidgetModel?.lockInAnswer(optionsItem.id!!)",
      "language": "kotlin"
    }
  ]
}
[/block]
***VoteResults***
The VoteResults gives you events for updates on the Quiz Widget. The event contains the vote count changes for each option on the server.
[block:code]
{
  "codes": [
    {
      "code": "quizWidgetModel?.voteResults?.subscribe(this) { result ->\n                    val op =\n                        result?.choices?.find { option -> option.id == adapter.getSelectedOption()?.id }\n\n                    op?.let { option ->\n                        Toast.makeText(\n                            context, when (option.is_correct) {\n                                true -> \"Correct\"\n                                else -> \"Incorrect\"\n                            }, Toast.LENGTH_SHORT\n                        ).show()\n                    }\n                    \n                }",
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
      "code": "  quizWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<QuizWidgetUserInteraction>>(){\n            override fun onResponse(result: List<QuizWidgetUserInteraction>?, error: String?) {\n            \n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sample Custom Quiz Widget"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "package com.livelike.livelikedemo.customwidgets\n\nimport android.content.Context\nimport android.graphics.Color\nimport android.support.constraint.ConstraintLayout\nimport android.support.v7.widget.RecyclerView\nimport android.util.AttributeSet\nimport android.view.LayoutInflater\nimport android.view.View\nimport android.view.ViewGroup\nimport android.widget.Toast\nimport com.bumptech.glide.Glide\nimport com.livelike.engagementsdk.OptionsItem\nimport com.livelike.engagementsdk.widget.widgetModel.QuizWidgetModel\nimport com.livelike.livelikedemo.R\nimport kotlinx.android.synthetic.main.custom_quiz_widget.view.button2\nimport kotlinx.android.synthetic.main.custom_quiz_widget.view.imageView2\nimport kotlinx.android.synthetic.main.custom_quiz_widget.view.rcyl_quiz_list\nimport kotlinx.android.synthetic.main.quiz_image_list_item.view.imageButton2\nimport kotlinx.android.synthetic.main.quiz_image_list_item.view.textView8\nimport kotlinx.android.synthetic.main.quiz_list_item.view.button4\nimport kotlinx.android.synthetic.main.quiz_list_item.view.textView7\n\nclass CustomQuizWidget : ConstraintLayout {\n    var quizWidgetModel: QuizWidgetModel? = null\n    var isImage = false\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_quiz_widget, this@CustomQuizWidget)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        quizWidgetModel?.widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.choices?.let {\n                val adapter =\n                    QuizListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))\n                rcyl_quiz_list.adapter = adapter\n                button2.setOnClickListener {\n                    adapter.getSelectedOption()?.let { item ->\n                        if (adapter.optionIdCount.isEmpty())\n                            quizWidgetModel?.lockInAnswer(item.id!!)\n                    }\n                }\n                quizWidgetModel?.voteResults?.subscribe(this) { result ->\n                    val op =\n                        result?.choices?.find { option -> option.id == adapter.getSelectedOption()?.id }\n\n                    op?.let { option ->\n                        Toast.makeText(\n                            context, when (option.is_correct) {\n                                true -> \"Correct\"\n                                else -> \"Incorrect\"\n                            }, Toast.LENGTH_SHORT\n                        ).show()\n                    }\n                    result?.choices?.let { options ->\n                        options.forEach { op ->\n                            adapter.optionIdCount[op.id] = op.answer_count ?: 0\n                        }\n                        adapter.notifyDataSetChanged()\n                    }\n                }\n            }\n            imageView2.setOnClickListener {\n                quizWidgetModel?.finish()\n            }\n\n        }\n\n    }\n\n    override fun onDetachedFromWindow() {\n        super.onDetachedFromWindow()\n        quizWidgetModel?.voteResults?.unsubscribe(this)\n    }\n}\n\nclass QuizListAdapter(\n    private val context: Context,\n    private val isImage: Boolean,\n    val list: ArrayList<OptionsItem>\n) :\n    RecyclerView.Adapter<QuizListAdapter.QuizListItemViewHolder>() {\n    private var selectedIndex = -1\n    val optionIdCount: HashMap<String, Int> = hashMapOf()\n    fun getSelectedOption(): OptionsItem? = when (selectedIndex > -1) {\n        true -> list[selectedIndex]\n        else -> null\n    }\n\n    class QuizListItemViewHolder(view: View) : RecyclerView.ViewHolder(view)\n\n    override fun onCreateViewHolder(p0: ViewGroup, p1: Int): QuizListItemViewHolder {\n        return QuizListItemViewHolder(\n            LayoutInflater.from(p0.context!!).inflate(\n                when (isImage) {\n                    true -> R.layout.quiz_image_list_item\n                    else -> R.layout.quiz_list_item\n                }, p0, false\n            )\n        )\n    }\n\n    override fun onBindViewHolder(holder: QuizListItemViewHolder, index: Int) {\n        val item = list[index]\n        if (isImage) {\n            Glide.with(context)\n                .load(item.imageUrl)\n                .into(holder.itemView.imageButton2)\n            if (selectedIndex == index) {\n                holder.itemView.imageButton2.setBackgroundColor(Color.BLUE)\n            } else {\n                holder.itemView.imageButton2.setBackgroundColor(Color.GRAY)\n            }\n            holder.itemView.textView8.text = \"${optionIdCount[item.id!!] ?: 0}\"\n            optionIdCount[item.id!!]?.let {\n                if (selectedIndex == index) {\n                    if (item.isCorrect == true) {\n                        holder.itemView.imageButton2.setBackgroundColor(Color.GREEN)\n                    } else {\n                        holder.itemView.imageButton2.setBackgroundColor(Color.RED)\n                    }\n                }\n            }\n            holder.itemView.imageButton2.setOnClickListener {\n                if (optionIdCount[item.id!!] == null) {\n                    selectedIndex = holder.adapterPosition\n                    notifyDataSetChanged()\n                }\n            }\n        } else {\n            holder.itemView.textView7.text = \"${optionIdCount[item.id!!] ?: 0}\"\n            holder.itemView.button4.text = \"${item.description}\"\n            if (selectedIndex == index) {\n                holder.itemView.button4.setBackgroundColor(Color.BLUE)\n            } else {\n                holder.itemView.button4.setBackgroundColor(Color.GRAY)\n            }\n            optionIdCount[item.id!!]?.let {\n                if (selectedIndex == index) {\n                    if (item.isCorrect == true) {\n                        holder.itemView.button4.setBackgroundColor(Color.GREEN)\n                    } else {\n                        holder.itemView.button4.setBackgroundColor(Color.RED)\n                    }\n                }\n            }\n            holder.itemView.button4.setOnClickListener {\n                if (optionIdCount[item.id!!] == null) {\n                    selectedIndex = holder.adapterPosition\n                    notifyDataSetChanged()\n                }\n            }\n        }\n\n    }\n\n    override fun getItemCount(): Int = list.size\n}\n",
      "language": "kotlin"
    }
  ]
}
[/block]