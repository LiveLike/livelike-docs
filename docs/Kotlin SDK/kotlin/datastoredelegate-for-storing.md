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

## Using DataStoreDelegate

```kotlin
class DataStoreDelegateKotlinImpl:DataStoreDelegate{
  override fun setNickname(nickName: String) {
       //store nickname
    }

    override fun getNickname(): String {
        //get nickname from storage
    }

    override fun getAccessToken(): String? {
        //store accesstoken
    }

    override fun setAccessToken(accessToken: String) {
        //return accesstoken
    }

    override fun getChatRoomMessageReceived(): String? {
       // return chat room msg received
    }

    override fun setChatRoomMessageReceived(data: String) {
        //store chat room msg received
    }

    override fun getWidgetClaimToken(): String? {
        // get claim token 
    }

    override fun setWidgetClaimToken(token: String) {
        //store claim token received
    }

    override fun addPublishedMessage(channel: String, messageId: String) {
        //store messages for particular channel
    }

    override fun flushPublishedMessage(vararg channels: String) {
        //flush messages
    }

    override fun getPublishedMessages(channel: String): MutableSet<String> {
        // return stored published message on a channel
    }

    override fun addWidgetPredictionVoted(id: String, optionId: String) {
       //store voted prediction widget id and optionId

    }

    override fun getWidgetPredictionVoted(): Array<SavedWidgetVote> {
        // return saved voted prediction widget
    }

    override fun getWidgetPredictionVotedAnswerIdOrEmpty(id: String?): String {
       // store prediction id voted
    }

    override fun addPoints(points: Int) {
       //store points
    }

    override fun getTotalPoints(): Int {
        //return points
    }

    override fun shouldShowPointTutorial(): Boolean {
       //store, if need to show points tutorial
    }

    override fun pointTutorialSeen() {
        // return if point tutorial seen
    }

    override fun addWidgetNumberPredictionVoted(
        id: String,
        widgetVoteList: List<NumberPredictionVotes>
    ) {
        //store voted number prediction votes(id and number)
    }

    override fun getWidgetNumberPredictionVoted(): Array<NumberPredictionSavedWidgetVote> {
        //return stored number prediction votes
    }
}
```

You can pass this as a param on SDK init.

```kotlin
var sdk = LiveLikeKotlin(
        clientId = "8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS",
        dataStoreDelegate = DataStoreDelegateKotlinImpl(),
        mainDispatcher = Dispatchers.Default
    )
```
