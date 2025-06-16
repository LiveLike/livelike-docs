---
title: Building a Text Ask Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building a Text Ask Widget | Android SDK | LiveLike
  description: >-
    This is a guide on building a Text Ask Widget for Android applications.
    Check out the Text Ask Widget Model to learn more.
  robots: index
next:
  description: ''
---
> 📘 Minimum SDK version
>
> 2.22

This is a guide on building a custom Text Ask Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Text Ask Widget Model

The Text Ask Widget Model is like a ViewModel for Text Ask Widget.

***Text Ask Data(object of LiveLikeWidget class)***\
The Text Ask Data provides data about the Text Ask Widget such as the title text, prompt and the confirmation message.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

```kotlin
askWidgetModel?.widgetData?.let { liveLikeWidget ->
            title.text="${liveLikeWidget.title}"
            prompt.text="${liveLikeWidget.prompt}"
            confirmationMessage.text="${liveLikeWidget.confirmationMessage}"
 }
```

***Submit Reply***

For submitting your reply to the backend, the widget model contains a method "submitReply(reply)" which needed reply to send to the backend for locking/submitting the answer. The reply string which you will be submitting has a character limit of 240.

Note: Once the reply is locked in the backend, it cannot be changed/updated for that ask widget.

```kotlin
askWidgetModel?.submitReply(reply)
```

***Interaction History***\
To load the interaction history (retrieve the response you submitted), you can call the loadInteractionHistory method\
Eg:

```kotlin
askWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<TextAskUserInteraction>>(){
            override fun onResponse(result: List<TextAskUserInteraction>?, error: String?) {
            
            }
        })
```

## Sample Text Ask Widget

```kotlin
class CustomTextAskWidget : ConstraintLayout{

    var askModel: TextAskWidgetModel? = null

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
        inflate(context, R.layout.custom_text_ask_widget, this)
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        askModel?.widgetData?.let { liveLikeWidget ->
        titleTv.text = liveLikeWidget.title
        promptTv.text = liveLikeWidget.prompt
        confirmationMessageTv.text = liveLikeWidget.confirmation_message
        confirmationMessageTv.visibility = GONE  
         userInputEdt.addTextChangedListener(object : TextWatcher {
                override fun afterTextChanged(arg0: Editable) {
                    if (userInputEdt.isEnabled) enableSendBtn() // send button is enabled
                }

                override fun beforeTextChanged(
                    s: CharSequence,
                    start: Int,
                    count: Int,
                    after: Int
                ) {
                }

                override fun onTextChanged(s: CharSequence, start: Int, before: Int, count: Int) {}
            })
          
         sendBtn.setOnClickListener {
            if (userInputEdt.text.toString().trim().isNotEmpty()) {
                    disableUserInput()// user input edit text disbaled
                    disableSendBtn() // send button disbaled
                    askWidgetModel?.submitReply(userInputEdt.text.toString().trim())
                    hideKeyboard()
                    confirmationMessageTv.visibility = VISIBLE
                }
            }
         }
    }
}
```
