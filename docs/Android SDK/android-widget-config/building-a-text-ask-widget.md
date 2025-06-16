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
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK version",
  "body": "2.22"
}
[/block]
This is a guide on building a custom Text Ask Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Text Ask Widget Model"
}
[/block]
The Text Ask Widget Model is like a ViewModel for Text Ask Widget.

***Text Ask Data(object of LiveLikeWidget class)***
The Text Ask Data provides data about the Text Ask Widget such as the title text, prompt and the confirmation message.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

[block:code]
{
  "codes": [
    {
      "code": "askWidgetModel?.widgetData?.let { liveLikeWidget ->\n            title.text=\"${liveLikeWidget.title}\"\n            prompt.text=\"${liveLikeWidget.prompt}\"\n            confirmationMessage.text=\"${liveLikeWidget.confirmationMessage}\"\n }  ",
      "language": "kotlin"
    }
  ]
}
[/block]
***Submit Reply***

For submitting your reply to the backend, the widget model contains a method "submitReply(reply)" which needed reply to send to the backend for locking/submitting the answer. The reply string which you will be submitting has a character limit of 240.

Note: Once the reply is locked in the backend, it cannot be changed/updated for that ask widget.
[block:code]
{
  "codes": [
    {
      "code": "askWidgetModel?.submitReply(reply)",
      "language": "kotlin"
    }
  ]
}
[/block]
***Interaction History***
To load the interaction history (retrieve the response you submitted), you can call the loadInteractionHistory method
Eg:
[block:code]
{
  "codes": [
    {
      "code": " askWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<TextAskUserInteraction>>(){\n            override fun onResponse(result: List<TextAskUserInteraction>?, error: String?) {\n            \n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sample Text Ask Widget"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomTextAskWidget : ConstraintLayout{\n\n    var askModel: TextAskWidgetModel? = null\n\n    constructor(context: Context) : super(context) {\n        init(null, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init(attrs, 0)\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init(attrs, defStyle)\n    }\n\n    private fun init(attrs: AttributeSet?, defStyle: Int) {\n        inflate(context, R.layout.custom_text_ask_widget, this)\n    }\n\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        askModel?.widgetData?.let { liveLikeWidget ->\n        titleTv.text = liveLikeWidget.title\n        promptTv.text = liveLikeWidget.prompt\n        confirmationMessageTv.text = liveLikeWidget.confirmation_message\n        confirmationMessageTv.visibility = GONE  \n         userInputEdt.addTextChangedListener(object : TextWatcher {\n                override fun afterTextChanged(arg0: Editable) {\n                    if (userInputEdt.isEnabled) enableSendBtn() // send button is enabled\n                }\n\n                override fun beforeTextChanged(\n                    s: CharSequence,\n                    start: Int,\n                    count: Int,\n                    after: Int\n                ) {\n                }\n\n                override fun onTextChanged(s: CharSequence, start: Int, before: Int, count: Int) {}\n            })\n          \n         sendBtn.setOnClickListener {\n            if (userInputEdt.text.toString().trim().isNotEmpty()) {\n                    disableUserInput()// user input edit text disbaled\n                    disableSendBtn() // send button disbaled\n                    askWidgetModel?.submitReply(userInputEdt.text.toString().trim())\n                    hideKeyboard()\n                    confirmationMessageTv.visibility = VISIBLE\n                }\n            }\n         }\n    }\n}",
      "language": "kotlin"
    }
  ]
}
[/block]