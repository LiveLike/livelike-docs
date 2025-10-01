---
title: Prediction Game Tutorial
excerpt: How to make a fantasy prediction game using the LiveLike SDK
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: rewards
      title: Rewards
    - type: basic
      slug: leaderboards
      title: Leaderboards
---
You can create a fantasy prediction game using the LiveLike SDK. This tutorial will explain the process of building an app where users can make their predictions and then earn points for each correct one. You'll learn how to how to publish prediction widgets, set up leaderboards and rewards, and how to customize the user experience of earning rewards.

In just a few steps, you'll be able to create a fantasy prediction game using components provided by the LiveLike SDK:

1. Create an app if you haven't already
2. Create a reward item for points
3. Create a reward table for automatically give points for correct predictions
4. Create a leaderboard for users to compete on
5. Create a program and link it with the reward table and leaderboard
6. Send prediction widgets to the program
7. Send correct predictions as follow-up widgets

## Getting Started

If you haven't already, you need to create an <Glossary>App</Glossary> and get your <Glossary>Client ID</Glossary>. Follow the guide at [Retrieving Important Keys](doc:retrieving-important-keys) and come back here once you have your Client ID. You should also be ready to add the LiveLike SDK as a dependency to your project.

## Setting Up Points

You will need to create a Reward Item in the system for users to earn. We'll be calling it "Points" in this tutorial, and our goal is to have users earn Points for each correct prediction. Head over to your app on the [Producer Site](https://cf-blast.livelikecdn.com/producer/) and:

1. Navigate to the *Rewards* section in the sidebar
2. Switch to the *Items* tab and press the *New Reward Item* button
3. Name the new item "Points" and save it

Now you have an item called Points that users can earn. For them to be earned automatically by users when they make correct predictions, you have to set up a Reward Table. Still inside the Rewards section:

1. Switch to the *Tables* tab and press the *New Reward Table* button
2. Name the new table "Fantasy Predictions" and save it
3. Click on the newly created Fantasy Predictions table
4. Press the "New Reward Table Entry" button
5. Set the new entry's reward item to Points, the action to *Made a correct prediction*, the amount to 100, and save it

Now you have a reward table that will automatically give 100 Points to every user that makes a correct prediction. You probably noticed there are other actions, but we won't need them for this tutorial.

## Setting Up Leaderboards

Users can be competitive, and an easy way to let them play against each other is to rank them on a leaderboard. Let's create a leaderboard in the Producer Site now:

1. Navigate to the *Leaderboards* section from the sidebar
2. Press the *New Leaderboard* button
3. Name the new leaderboard "Fantasy Leaders" and save it

## Setting Up Programs

A <Glossary>Program</Glossary> usually corresponds to an individual game, episode, or event. Programs can be linked to reward tables and leaderboards. All user rewards for a program are determined by its linked reward tables, and any rewards earned contribute to users' ranks in its linked leaderboards. 

1. Navigate to the *Programs* section from the sidebar
2. Press the *New Program* button
3. Name the new program "First Fantasy Game" and save it
4. Link the "Fantasy Predictions" reward table to the new program
5. Link the "Fantasy Leaders" leaderboard to the new program

## Designing the Gameplay

Once you have everything set up in the Producer site, it's time to design the gameplay. There are lots of ways to make a fun prediction game, but there are a couple popular styles that LiveLike was designed for, like pick 'em and in-play. These styles can be used together or separately in your implementation, it's up to you to design the game by mixing and matching the LiveLike features.

### Pick 'Em Style

Pick 'em predictions are made before the game starts, and once it starts users predictions are locked in. In this experience, users are presented with a list of picks to make, usually around ten or so. Each prediction asks questions with a few distinct possibilities, like:

* Who will win?
* Will this player score before halftime?
* Will this team score more than 2 goals?

You can build this experience by creating a dedicated screen for each game to make picks from.  Publish a set of 6-10 predictions before the game, and only allow users to make predictions before the game is live. Allow users to return to the screen to check their progress and claim any rewards they earned.

### In-Play Style

In-play predictions are made throughout the game, after it has already started. The questions are often asked on the fly, and users only have a limited amount of time to answer. Some example predictions that could be made are:

* Will the next play be a run, pass, or kick?
* Will this VAR challenge be overturned?
* Will this player score more than 15 points this quarter?

You can build this experience by allowing widgets to pop in and out as users watch the game. 

## Sending Predictions

Now that you have a program set up with automatic rewards and leaderboards, and have your basic experience design established, you can start sending prediction widgets to users. Every user who makes correct predictions will earn points and gain ranks on the leaderboard.

The prediction experience is actually made up of two widgets: a prediction widget, and a prediction follow-up widget. The prediction widget displays the question and the options to choose from, and accepts user input. The follow-up widget confirms the correct option, and gives rewards for being correct. To send a prediction:

1. Navigate to the "First Fantasy Game" program
2. Switch to the *Create* tab if you aren't already on it
3. Press the "New Prediction" button
4. Think of something to ask the audience, and a couple possibilities
5. Fill in the question and the options based on your idea
6. Press *Publish* to send the prediction to users

Now any user who sees that prediction widget can make their prediction. Depending on the experience you build, users might have to go to a dedicated screen to see a list of widgets to interact with, or widgets might pop up immediately on the same screen they are watching on. Once you know the outcome of the prediction, it's time to send the follow-up:

1. Switch to the *Pending* tab
2. Find and click on the follow-up widget that was automatically created when you published the prediction
3. Mark the correct prediction
4. Press *Publish* to send the follow-up to users

Congratulations! All the users who made correct predictions are now eligible to earn the points rewards associated with it.

> 📘 Automating predictions
>
> It is possible to automate the prediction publishing process using the LiveLike REST API. If you have access to a game data feed, you can develop a solution that drives the LiveLike API based on the events coming through in the data feed. This is a good option for complex game rules, or for teams that don't have the resources to send the predictions manually.

## Customizing the Experience

By default, the EngagementSDK will store the Claim Token in the device storage (iOS, Android) or in the browser cache (Web). If the user uninstalls the application or clears their stored app data then they Claim Token will be lost and the user will miss out on potential rewards. You can override where the Claim Token is stored with the steps below:

```swift
class MyViewController: UIViewController {
  let sdk: EngagementSDK
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    // Implement PredictionVoteRepository then set it in the EngagementSDKConfig
    var sdkConfig = EngagementSDKConfig(clientID: "my-client-id")
    sdkConfig.widget.predictionVoteRepo = self
    sdk = EngagementSDK(config: sdkConfig)
  }
}

extension MyViewController: PredictionVoteRepository {
  func get(by widgetID: String, completion: @escaping (PredictionVote?) -> Void) {
    // This is called when the EngagementSDK attempts to claim a prediction follow-up reward
    // Load the PredictionVote from your database (or other persistent storage)
    // Then call the completion block
    // Upon failure to load the PredictionVote you can call `completion(nil)`
  }

  func add(vote: PredictionVote, completion: @escaping (Bool) -> Void) {
    // This is called when the EngagementSDK attempts to store the user's prediction vote details
    // Store the PredictionVote in your database (or other persisten storage)
    // When successfully stored, call `completion(true)`
    // Upon failure to store the Prediction vote you can call `completion(false)`
  }
}
```
```kotlin
EngagementSDK.predictionWidgetVoteRepository = LiveLikePredictionWidgetVoteRepository()

class LiveLikePredictionWidgetVoteRepository : PredictionWidgetVoteRepository {


    override fun add(vote: PredictionWidgetVote, completion: () -> Unit) {
    // This is called when the EngagementSDK attempts to store the user's prediction vote details
    // Store the PredictionVote in your database (or other persisten storage)
    // When successfully stored, call `completion(true)`
    // Upon failure to store the Prediction vote you can call `completion(false)`
    }

    override fun get(predictionWidgetID: String) : String? {
     // This is called when the EngagementSDK attempts to claim a prediction follow-up reward
    // Load the PredictionVote from your database (or other persistent storage)
    // Then call the completion block
    // Upon failure to load the PredictionVote you can call `completion(nil)`
    }

}
```
