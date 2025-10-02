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
## Customize Snap to Live button in stock chat UI

Integrator can implement ChatSnapToLiveDelegate to pass his own snap to live view with ConstraintSet. See the sample code below.

```kotlin
val chatSnapToLiveDelegate = object : ChatSnapToLiveDelegate {
                val snapToLiveCard = DemoSnapToLiveBinding.inflate(
                    LayoutInflater.from(this@ExoPlayerActivity),
                    null,
                    false
                )

                override fun getSnapToLiveView(): View {
                    return snapToLiveCard.root
                }

                override fun applyConstraintsOnChatViewForSnapToLiveView(
                    constraintSet: ConstraintSet,
                    rootViewId: Int
                ) {
                    constraintSet.connect(
                        getSnapToLiveView().id,
                        ConstraintSet.START,
                        ConstraintSet.PARENT_ID,
                        ConstraintSet.START
                    )
                    constraintSet.connect(
                        getSnapToLiveView().id,
                        ConstraintSet.BOTTOM,
                        ConstraintSet.PARENT_ID,
                        ConstraintSet.BOTTOM
                    )
                    constraintSet.connect(
                        getSnapToLiveView().id,
                        ConstraintSet.END,
                        ConstraintSet.PARENT_ID,
                        ConstraintSet.END
                    )
                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
                        constraintSet.setHorizontalBias(
                            getSnapToLiveView().id,
                            0.5f
                        )
                    } else {
                        constraintSet.setHorizontalBias(
                            getSnapToLiveView().id,
                            0.5f
                        )
                    }
                    constraintSet.setMargin(
                        getSnapToLiveView().id,
                        ConstraintSet.START,
                        resources.getDimensionPixelSize(com.livelike.engagementsdk.R.dimen.livelike_snap_live_margin_start)
                    )
                    constraintSet.setMargin(
                        getSnapToLiveView().id,
                        ConstraintSet.LEFT,
                        resources.getDimensionPixelSize(com.livelike.engagementsdk.R.dimen.livelike_snap_live_margin_left)
                    )
                    constraintSet.setMargin(
                        getSnapToLiveView().id,
                        ConstraintSet.END,
                        0
                    )
                    constraintSet.setMargin(
                        getSnapToLiveView().id,
                        ConstraintSet.RIGHT,
                        0
                    )
                    constraintSet.setMargin(
                        getSnapToLiveView().id,
                        ConstraintSet.BOTTOM,
                        350
                    )
                }
            }
            binding.chatWidget.chatView.setChatSnapToLiveDelegate(chatSnapToLiveDelegate)
```

## Customize Scrollbar in Stock Chat UI

Integrator can customize the scrollbar of the stock Chat UI with their own drawable. See the sample code below.

> 📘 This is only applicable for Android 10 (API level 29) and above

```kotlin
binding.chatWidget.chatView.setScrollBarEnabled(isScrollBarNeeded=true,
                                                scrollbarDrawable = AppCompatResources.getDrawable(this,android.R.color.darker_gray))
```

## Insert custom content between messages in Stock Chat UI

```kotlin
binding.chatWidget.chatView.chatViewSeparatorContentDelegate =
                object : ChatViewSeparatorContentDelegate {
                    override fun getSeparatorView(
                        messageTop: LiveLikeChatMessage?,
                        messageBottom: LiveLikeChatMessage?
                    ): View? {
                        var separatorViewBinding: DemoChatDateViewBinding? =
                            DemoChatDateViewBinding.inflate(
                                LayoutInflater.from(this@ExoPlayerActivity),
                                null,
                                false
                            )

                        val today = ZonedDateTime.now()
                        val yesterday = today.minusDays(1)
                        val b = messageBottom?.createdAt?.parseISODateTime()
                        val mBottom = if (b != null) ZonedDateTime.ofInstant(
                            b.toInstant(),
                            ZoneId.systemDefault()
                        )?.dayOfMonth
                        else null
                        val t = messageTop?.createdAt?.parseISODateTime()
                        val mTop = if (t != null)
                            ZonedDateTime.ofInstant(
                                t.toInstant(),
                                ZoneId.systemDefault()
                            )?.dayOfMonth
                        else null
                        //println("ExoPlayerActivity.getSeparatorView>>$mBottom >> $mTop >> ${today.dayOfMonth} >>${yesterday.dayOfMonth} >> ${messageTop?.message} >> ${messageBottom?.message}")
                        if (messageTop == null) {
                            separatorViewBinding?.txtDate?.text = when {
                                today.dayOfMonth == mBottom -> "Today"
                                yesterday.dayOfMonth == mBottom -> "Yesterday"
                                else -> messageBottom?.createdAt?.parseISODateTime()
                                    ?.toLocalDateTime()?.format(
                                        DateTimeFormatter.ISO_LOCAL_DATE
                                    )
                            }
                        } else if (mTop == mBottom) {
                            separatorViewBinding = null
                        } else {
                            when {
                                today.dayOfMonth == mBottom -> separatorViewBinding?.txtDate?.text =
                                    "Today"
                                yesterday.dayOfMonth == mBottom -> separatorViewBinding?.txtDate?.text =
                                    "Yesterday"
                                messageBottom?.createdAt != null -> separatorViewBinding?.txtDate?.text =
                                    messageBottom?.createdAt?.parseISODateTime()?.format(
                                        DateTimeFormatter.ISO_LOCAL_DATE
                                    )
                                else -> {
                                    separatorViewBinding = null
                                }
                            }
                        }
                        if (messageBottom?.createdAt?.parseISODateTime()?.toLocalDateTime()
                                ?.isAfter(
                                    lastMessageTime?.parseISODateTime()?.toLocalDateTime()
                                ) == true
                        ) {
                            if (messageTop?.createdAt?.parseISODateTime()?.toLocalDateTime()
                                    ?.isAfter(
                                        (lastMessageTime?.parseISODateTime()?.toLocalDateTime())
                                    ) != true
                            ) {
                                val separatorViewBinding2 = DemoChatDateViewBinding.inflate(
                                    LayoutInflater.from(this@ExoPlayerActivity),
                                    null,
                                    false
                                )
                                separatorViewBinding2.txtDate.text = "New Messages"
                                val linearLayout = LinearLayout(this@ExoPlayerActivity)
                                linearLayout.orientation = LinearLayout.VERTICAL
                                separatorViewBinding?.let {
                                    linearLayout.addView(
                                        separatorViewBinding.root
                                    )
                                }
                                linearLayout.addView(separatorViewBinding2.root)
                                return linearLayout
                            }
                        }
                        return separatorViewBinding?.root
                    }
                }
```
