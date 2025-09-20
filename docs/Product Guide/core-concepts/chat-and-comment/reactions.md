---
title: Reactions
deprecated: false
hidden: false
metadata:
  robots: index
---
Reactions let fans instantly express how they feel about content — whether it’s cheering for a team, liking a message, or showing support during a big moment.
With LiveLike, any content that has a unique identifier can support reaction: chat messages, blog posts, comments, videos, polls, or your own custom items.

<Image align="center" width="300px" src="https://files.readme.io/a165ca3-ReactionsAsAService.png" />

> 📘 Available since:
>
> * **Web SDK** `2.29.0`
> * **Android SDK** `2.54`
> * **iOS SDK** `2.51`

***

### Core Concepts

* **Reaction Pack**
  A collection of reaction types (each with an ID, name, and asset). Packs define the available reactions and can be linked to specific spaces.

* **Reaction Space**
  A namespace that maps your content to reaction packs. Each space contains _targets_ (individual items like chat messages, blog comments, or video moments) that users can react to.

* **User Reaction**
  A single instance of a user reacting to a target inside a reaction space.

***

### Typical Workflow

1. **Create a Reaction Pack** – via Producer Suite or API.
2. **Create Reaction Spaces** – one per content unit (e.g. a chat room, video, blog post), linked with the right packs.
3. **Add User Reactions** – users select a reaction from a pack and attach it to a specific target (e.g. a message ID or video moment).

👉 Example:

* In video apps, the target group ID = video ID, targets = video moments.
* In chat apps, the target group ID = chat room ID, targets = message IDs.

***

## Why Use Reactions?

* **Instant Engagement** – give users lightweight ways to interact beyond chat.
* **Content-Specific Customization** – holiday themes, team-specific packs, sponsor-driven packs.
* **Exclusive Access** – reward loyalty tiers or premium members with special reaction packs.
* **Real-Time Feedback** – surface trends, bursts of excitement, and engagement insights.

***

## Exclusive Reaction Packs 🔒

Like stickers, reactions can also be **exclusive**.
Only specific users (based on profile rules) can access them — perfect for **tiered memberships, sponsor rewards, or collectible reaction sets**.

***

## APIs Overview (Developer Reference)

Reactions are exposed via three main APIs:

1. **Reaction Packs API** – create and manage sets of reaction types.
2. **Reaction Spaces API** – map content to packs and handle isolation between content.
3. **User Reactions API** – add, remove, and query user reactions.

> Expand below for SDK examples in **Web, Android, iOS** 👇

<details>
  <summary>Reaction Packs API</summary>

  #### List Reaction Packs

  This could be used to get list of reaction pack created through producer suite.

  ```javascript
  LiveLike.getReactionPacks().then(({results}) => console.log(results))
  ```
  ```kotlin
    engagementSDK.reaction().getReactionPacks(LiveLikePagination.FIRST,
              object : LiveLikeCallback<List<ReactionPack>>() {
                  override fun onResponse(result: List<ReactionPack>?, error: String?) {
                      result?.let {
                          //handle success block}
                      }
                      error?.let {
                          //handle failure block
                      }
                  })
  ```
  ```swift
  sdk.reaction.getReactionPacks(page: .first) { result in
  	switch result {
      case .success(let reactionPacks):
      	//Success Block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```

  ####

  #### Get Reaction Pack Details

  This could be used to get reaction pack details using reaction pack Id.

  ```javascript
  LiveLike.getReactionPackDetail({
      reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
  }).then(reactionPack => console.log(reactionPack))
  ```
  ```kotlin
   engagementSDK.reaction()
              .getReactionPackDetails(< reaction -pack - id >, object: LiveLikeCallback<ReactionPack>(){
              override fun onResponse(result: ReactionPack?, error: String?) {
                  result?.let {
                      //handle success
                  }

                  error?.let {
                      //handle error
                  }
              }
              )
  ```
  ```swift
  sdk.reaction.getReactionPackInfo(reactionPackID: packID) { result in
  	switch result {
  		case .success(let reactionPack):
      	//Success block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```

  ###
</details>

<details>
  <summary>Reaction Spaces API</summary>

  ... (existing code snippets)
</details>

<details>
  <summary>User Reactions API</summary>

  ... (existing code snippets)
</details>

***

## Real-Time Events

Developers can subscribe to **real-time events** such as:

* `ADD_REACTION` – when a user reacts.
* `REMOVE_REACTION` – when a user removes their reaction.
* `UPDATE_REACTION_SPACE` – when packs linked to a space change.

SDK delegates and listeners are available across **Web, Android, and iOS**.

***

## Example Use Cases

* ❤️ React to specific **chat messages** in a live chat.
* 🎬 Show excitement during **video highlights** or time-coded moments.
* 📝 Add reactions to **comments on blog posts**.
* 🎉 Provide **exclusive sponsor-branded reactions** for premium fans.

***

👉 In short: **Reactions make every piece of content more interactive, expressive, and fun.**
They’re lightweight for users, flexible for integrators, and powerful for PMs to drive engagement and monetization.
