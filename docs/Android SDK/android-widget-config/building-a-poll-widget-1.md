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
> 📘 Minimum SDK Version
>
> 2.9

This is a guide on building a custom Poll Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Poll Widget Model

The Poll Widget Model is like a ViewModel for Poll Widget.

***Poll Data(object of LiveLikeWidget class)***\
The Poll Data provides data about the Poll Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in livelikeWidget class for the poll.

```kotlin
pollWidgetModel?.widgetData?.let { liveLikeWidget ->
            liveLikeWidget.options?.let {
                if (it.size > 2) {
                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)
                }
                val adapter =
                    PollListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))
                rcyl_poll_list.adapter = adapter
                adapter.pollListener = object : PollListAdapter.PollListener {
                    override fun onSelectOption(id: String) {
                        pollWidgetModel?.submitVote(id)
                    }
                }
                button2.visibility = View.GONE
            }
        }
```

***SubmitVote***\
For submitting or changing the vote on the option for the poll which needed optionId to send to the backend for changing/submitting the vote for the poll.

```kotlin
pollWidgetModel?.submitVote(optionId)
```

***VoteResults***\
The VoteResults gives you events for updates on the Poll Widget. The event contains the vote count changes for each option on the server.

```kotlin
pollWidgetModel?.voteResults?.subscribe(this) { result ->
                    result?.choices?.let { options ->
                        options.forEach { op ->
                            adapter.optionIdCount[op.id] = op.vote_count ?: 0
                        }
                        adapter.notifyDataSetChanged()
                    }
                }
```

***Interaction History***\
To load the interaction history, you can call the loadInteractionHistory method\
Eg:

```kotlin
pollWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<PollWidgetUserInteraction>>(){
            override fun onResponse(result: List<PollWidgetUserInteraction>?, error: String?) {
              
            }
        })
```

## Sample Custom Poll Widget

```kotlin
class CustomPollWidget : ConstraintLayout {
    var pollWidgetModel: PollWidgetModel? = null
    var isImage = false

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
        inflate(context, R.layout.custom_poll_widget, this@CustomPollWidget)
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        pollWidgetModel?.widgetData?.let { liveLikeWidget ->
            liveLikeWidget.options?.let {
                if (it.size > 2) {
                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)
                }
                val adapter =
                    PollListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))
                rcyl_poll_list.adapter = adapter
                adapter.pollListener = object : PollListAdapter.PollListener {
                    override fun onSelectOption(id: String) {
                        pollWidgetModel?.submitVote(id)
                    }
                }
                button2.visibility = View.GONE
                pollWidgetModel?.voteResults?.subscribe(this) { result ->
                    result?.choices?.let { options ->
                        options.forEach { op ->
                            adapter.optionIdCount[op.id] = op.vote_count ?: 0
                        }
                        adapter.notifyDataSetChanged()
                    }
                }
            }
            imageView2.setOnClickListener {
                pollWidgetModel?.finish()
            }

        }

    }

    override fun onDetachedFromWindow() {
        super.onDetachedFromWindow()
        pollWidgetModel?.voteResults?.unsubscribe(this)
    }
}

class PollListAdapter(
    private val context: Context,
    private val isImage: Boolean,
    val list: ArrayList<OptionsItem>
) :
    RecyclerView.Adapter<PollListAdapter.PollListItemViewHolder>() {
    private var selectedIndex = -1
    val optionIdCount: HashMap<String, Int> = hashMapOf()
    fun getSelectedOption(): OptionsItem? = when (selectedIndex > -1) {
        true -> list[selectedIndex]
        else -> null
    }

    var pollListener: PollListener? = null

    interface PollListener {
        fun onSelectOption(id: String)
    }

    class PollListItemViewHolder(view: View) : RecyclerView.ViewHolder(view)

    override fun onCreateViewHolder(p0: ViewGroup, p1: Int): PollListItemViewHolder {
        return PollListItemViewHolder(
            LayoutInflater.from(p0.context!!).inflate(
                when (isImage) {
                    true -> R.layout.quiz_image_list_item
                    else -> R.layout.quiz_list_item
                }, p0, false
            )
        )
    }

    override fun onBindViewHolder(holder: PollListItemViewHolder, index: Int) {
        val item = list[index]
        if (isImage) {
            Glide.with(context)
                .load(item.imageUrl)
                .into(holder.itemView.imageButton2)
            if (selectedIndex == index) {
                holder.itemView.imageButton2.setBackgroundColor(Color.BLUE)
            } else {
                holder.itemView.imageButton2.setBackgroundColor(Color.GRAY)
            }
            holder.itemView.textView8.text = "${optionIdCount[item.id!!] ?: 0}"

            holder.itemView.imageButton2.setOnClickListener {
                selectedIndex = holder.adapterPosition
                pollListener?.onSelectOption(item.id!!)
                notifyDataSetChanged()
            }
        } else {
            holder.itemView.textView7.text = "${optionIdCount[item.id!!] ?: 0}"
            holder.itemView.button4.text = "${item.description}"
            if (selectedIndex == index) {
                holder.itemView.button4.setBackgroundColor(Color.BLUE)
            } else {
                holder.itemView.button4.setBackgroundColor(Color.GRAY)
            }

            holder.itemView.button4.setOnClickListener {
                selectedIndex = holder.adapterPosition
                pollListener?.onSelectOption(item.id!!)
                notifyDataSetChanged()
            }
        }

    }

    override fun getItemCount(): Int = list.size
}
```
