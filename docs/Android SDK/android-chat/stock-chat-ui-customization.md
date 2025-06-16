---
title: Stock Chat UI Customization
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
[block:api-header]
{
  "title": "Customize Snap to Live button in stock chat UI"
}
[/block]
Integrator can implement ChatSnapToLiveDelegate to pass his own snap to live view with ConstraintSet. See the sample code below.
[block:code]
{
  "codes": [
    {
      "code": "val chatSnapToLiveDelegate = object : ChatSnapToLiveDelegate {\n                val snapToLiveCard = DemoSnapToLiveBinding.inflate(\n                    LayoutInflater.from(this@ExoPlayerActivity),\n                    null,\n                    false\n                )\n\n                override fun getSnapToLiveView(): View {\n                    return snapToLiveCard.root\n                }\n\n                override fun applyConstraintsOnChatViewForSnapToLiveView(\n                    constraintSet: ConstraintSet,\n                    rootViewId: Int\n                ) {\n                    constraintSet.connect(\n                        getSnapToLiveView().id,\n                        ConstraintSet.START,\n                        ConstraintSet.PARENT_ID,\n                        ConstraintSet.START\n                    )\n                    constraintSet.connect(\n                        getSnapToLiveView().id,\n                        ConstraintSet.BOTTOM,\n                        ConstraintSet.PARENT_ID,\n                        ConstraintSet.BOTTOM\n                    )\n                    constraintSet.connect(\n                        getSnapToLiveView().id,\n                        ConstraintSet.END,\n                        ConstraintSet.PARENT_ID,\n                        ConstraintSet.END\n                    )\n                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {\n                        constraintSet.setHorizontalBias(\n                            getSnapToLiveView().id,\n                            0.5f\n                        )\n                    } else {\n                        constraintSet.setHorizontalBias(\n                            getSnapToLiveView().id,\n                            0.5f\n                        )\n                    }\n                    constraintSet.setMargin(\n                        getSnapToLiveView().id,\n                        ConstraintSet.START,\n                        resources.getDimensionPixelSize(com.livelike.engagementsdk.R.dimen.livelike_snap_live_margin_start)\n                    )\n                    constraintSet.setMargin(\n                        getSnapToLiveView().id,\n                        ConstraintSet.LEFT,\n                        resources.getDimensionPixelSize(com.livelike.engagementsdk.R.dimen.livelike_snap_live_margin_left)\n                    )\n                    constraintSet.setMargin(\n                        getSnapToLiveView().id,\n                        ConstraintSet.END,\n                        0\n                    )\n                    constraintSet.setMargin(\n                        getSnapToLiveView().id,\n                        ConstraintSet.RIGHT,\n                        0\n                    )\n                    constraintSet.setMargin(\n                        getSnapToLiveView().id,\n                        ConstraintSet.BOTTOM,\n                        350\n                    )\n                }\n            }\n            binding.chatWidget.chatView.setChatSnapToLiveDelegate(chatSnapToLiveDelegate)",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Customize Scrollbar in Stock Chat UI"
}
[/block]
Integrator can customize the scrollbar of the stock Chat UI with their own drawable. See the sample code below.
[block:callout]
{
  "type": "info",
  "title": "This is only applicable for Android 10 (API level 29) and above"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "binding.chatWidget.chatView.setScrollBarEnabled(isScrollBarNeeded=true,\n                                                scrollbarDrawable = AppCompatResources.getDrawable(this,android.R.color.darker_gray))",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Insert custom content between messages in Stock Chat UI"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "  binding.chatWidget.chatView.chatViewSeparatorContentDelegate =\n                object : ChatViewSeparatorContentDelegate {\n                    override fun getSeparatorView(\n                        messageTop: LiveLikeChatMessage?,\n                        messageBottom: LiveLikeChatMessage?\n                    ): View? {\n                        var separatorViewBinding: DemoChatDateViewBinding? =\n                            DemoChatDateViewBinding.inflate(\n                                LayoutInflater.from(this@ExoPlayerActivity),\n                                null,\n                                false\n                            )\n\n                        val today = ZonedDateTime.now()\n                        val yesterday = today.minusDays(1)\n                        val b = messageBottom?.createdAt?.parseISODateTime()\n                        val mBottom = if (b != null) ZonedDateTime.ofInstant(\n                            b.toInstant(),\n                            ZoneId.systemDefault()\n                        )?.dayOfMonth\n                        else null\n                        val t = messageTop?.createdAt?.parseISODateTime()\n                        val mTop = if (t != null)\n                            ZonedDateTime.ofInstant(\n                                t.toInstant(),\n                                ZoneId.systemDefault()\n                            )?.dayOfMonth\n                        else null\n                        //println(\"ExoPlayerActivity.getSeparatorView>>$mBottom >> $mTop >> ${today.dayOfMonth} >>${yesterday.dayOfMonth} >> ${messageTop?.message} >> ${messageBottom?.message}\")\n                        if (messageTop == null) {\n                            separatorViewBinding?.txtDate?.text = when {\n                                today.dayOfMonth == mBottom -> \"Today\"\n                                yesterday.dayOfMonth == mBottom -> \"Yesterday\"\n                                else -> messageBottom?.createdAt?.parseISODateTime()\n                                    ?.toLocalDateTime()?.format(\n                                        DateTimeFormatter.ISO_LOCAL_DATE\n                                    )\n                            }\n                        } else if (mTop == mBottom) {\n                            separatorViewBinding = null\n                        } else {\n                            when {\n                                today.dayOfMonth == mBottom -> separatorViewBinding?.txtDate?.text =\n                                    \"Today\"\n                                yesterday.dayOfMonth == mBottom -> separatorViewBinding?.txtDate?.text =\n                                    \"Yesterday\"\n                                messageBottom?.createdAt != null -> separatorViewBinding?.txtDate?.text =\n                                    messageBottom?.createdAt?.parseISODateTime()?.format(\n                                        DateTimeFormatter.ISO_LOCAL_DATE\n                                    )\n                                else -> {\n                                    separatorViewBinding = null\n                                }\n                            }\n                        }\n                        if (messageBottom?.createdAt?.parseISODateTime()?.toLocalDateTime()\n                                ?.isAfter(\n                                    lastMessageTime?.parseISODateTime()?.toLocalDateTime()\n                                ) == true\n                        ) {\n                            if (messageTop?.createdAt?.parseISODateTime()?.toLocalDateTime()\n                                    ?.isAfter(\n                                        (lastMessageTime?.parseISODateTime()?.toLocalDateTime())\n                                    ) != true\n                            ) {\n                                val separatorViewBinding2 = DemoChatDateViewBinding.inflate(\n                                    LayoutInflater.from(this@ExoPlayerActivity),\n                                    null,\n                                    false\n                                )\n                                separatorViewBinding2.txtDate.text = \"New Messages\"\n                                val linearLayout = LinearLayout(this@ExoPlayerActivity)\n                                linearLayout.orientation = LinearLayout.VERTICAL\n                                separatorViewBinding?.let {\n                                    linearLayout.addView(\n                                        separatorViewBinding.root\n                                    )\n                                }\n                                linearLayout.addView(separatorViewBinding2.root)\n                                return linearLayout\n                            }\n                        }\n                        return separatorViewBinding?.root\n                    }\n                }",
      "language": "kotlin"
    }
  ]
}
[/block]