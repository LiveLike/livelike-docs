---
title: DataStoreDelegate for local storage
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
The DataStoreDelegate can be used for local storage on your end. Although we have provided the default implementation, in case you want to store on your end, you can use this delegate as a param on SDK init and store things on your end. 
[block:api-header]
{
  "title": "Using DataStoreDelegate"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class DataStoreDelegateKotlinImpl:DataStoreDelegate{\n  override fun setNickname(nickName: String) {\n       //store nickname\n    }\n\n    override fun getNickname(): String {\n        //get nickname from storage\n    }\n\n    override fun getAccessToken(): String? {\n        //store accesstoken\n    }\n\n    override fun setAccessToken(accessToken: String) {\n        //return accesstoken\n    }\n\n    override fun getChatRoomMessageReceived(): String? {\n       // return chat room msg received\n    }\n\n    override fun setChatRoomMessageReceived(data: String) {\n        //store chat room msg received\n    }\n\n    override fun getWidgetClaimToken(): String? {\n        // get claim token \n    }\n\n    override fun setWidgetClaimToken(token: String) {\n        //store claim token received\n    }\n\n    override fun addPublishedMessage(channel: String, messageId: String) {\n        //store messages for particular channel\n    }\n\n    override fun flushPublishedMessage(vararg channels: String) {\n        //flush messages\n    }\n\n    override fun getPublishedMessages(channel: String): MutableSet<String> {\n        // return stored published message on a channel\n    }\n\n    override fun addWidgetPredictionVoted(id: String, optionId: String) {\n       //store voted prediction widget id and optionId\n\n    }\n\n    override fun getWidgetPredictionVoted(): Array<SavedWidgetVote> {\n        // return saved voted prediction widget\n    }\n\n    override fun getWidgetPredictionVotedAnswerIdOrEmpty(id: String?): String {\n       // store prediction id voted\n    }\n\n    override fun addPoints(points: Int) {\n       //store points\n    }\n\n    override fun getTotalPoints(): Int {\n        //return points\n    }\n\n    override fun shouldShowPointTutorial(): Boolean {\n       //store, if need to show points tutorial\n    }\n\n    override fun pointTutorialSeen() {\n        // return if point tutorial seen\n    }\n\n    override fun addWidgetNumberPredictionVoted(\n        id: String,\n        widgetVoteList: List<NumberPredictionVotes>\n    ) {\n        //store voted number prediction votes(id and number)\n    }\n\n    override fun getWidgetNumberPredictionVoted(): Array<NumberPredictionSavedWidgetVote> {\n        //return stored number prediction votes\n    }\n}",
      "language": "kotlin"
    }
  ]
}
[/block]
You can pass this as a param on SDK init.
[block:code]
{
  "codes": [
    {
      "code": "var sdk = LiveLikeKotlin(\n        clientId = \"8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS\",\n        dataStoreDelegate = DataStoreDelegateKotlinImpl(),\n        mainDispatcher = Dispatchers.Default\n    )",
      "language": "kotlin"
    }
  ]
}
[/block]