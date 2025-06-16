---
title: Points Redemption
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
LiveLike already supported gamification features for a longer time. and now we are introducing more improvements to the gamification experience by adding a point redemption feature that will enable your customers can earn points by performing specific actions and use those points to redeem real currency, gift cards, coupons, and more.

[block:api-header]
{
  "title": "For example"
}
[/block]
Imaging your platform can reward points to your customers for doing actions such as registering on the platform, watching videos, inviting a friend, subscribing, completing a quest, answering a poll, and a lot more. then your customers can redeem their earned points as gift cards and claim them in a variety of brands. It will help your business retain customers, convert prospective customers into loyal customers, and more. Now all of these are possible with the LiveLike point redemption feature.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f9b7965-Infographic_v2.png",
        "Infographic v2.png",
        4112,
        2054,
        "#000000"
      ]
    }
  ]
}
[/block]
LiveLike enables point redemption by integrating Prizeout with CMS. Prizeout is an innovative withdrawal platform that gives users more purchasing power in the form of digital gift cards with bonus offers. Those who choose Prizeout withdrawals usually receive their gift cards via e-mail within minutes and can redeem them at mainstream retailers such as Airbnb, Apple, GameStop, Lowe’s, and more.


[block:api-header]
{
  "title": "How using Prizeout can benefit your brand?"
}
[/block]
It will benefit your customers by having the power of redeeming points in different types of options such as real gift cards. Partners have had a 25%+ cumulative increase in user retention, 95% of brands on the Prizeout platform offer a potential bonus value of up to 25%, and Withdrawal is a no-cost payments service.


[block:api-header]
{
  "title": "How to get started?"
}
[/block]
To start using this feature, first should complete Prizeout integration with LiveLike CMS and follow the steps from below to create a reward item with a monetization feature and use that item to reward for certain actions of a user.
[block:callout]
{
  "type": "warning",
  "body": "Make sure you have successfully integrated Prizeout with LiveLike to start using this feature If not, please check this <a href=\"https://docs.livelike.com/docs/prizeout-integration\" target=\"_blank\" />documentation</a> for the complete guide.",
  "title": "The first step to start using this feature"
}
[/block]

[block:api-header]
{
  "title": "Create a monetization-enabled reward item"
}
[/block]
Let’s see how to create a reward item with Prizeout for monetization feature.


1. Navigate to **Rewards** > **New Reward Item** to start creating a new reward item.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/240c67f-Reward_Items.png",
        "Reward Items.png",
        1440,
        901,
        "#000000"
      ]
    }
  ]
}
[/block]
2. Add an image or symbol for the item and enter a name for the reward item in the **Name** input field.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ca981c0-New_Reward_Item_-_Set_PrizeOut_Point.png",
        "New Reward Item - Set PrizeOut Point.png",
        1440,
        901,
        "#000000"
      ]
    }
  ]
}
[/block]
3. Turn on the **Prizeout Points** switch.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4c56c50-set-conversion.png",
        "set-conversion.png",
        1440,
        901,
        "#000000"
      ]
    }
  ]
}
[/block]
4. To set the conversion rate, Enter the **Reward Item Amount** and the **Prizout Points** equal to that Reward Item.


[block:callout]
{
  "type": "info",
  "body": "1 Prizeout Point = 1 cent that you are rewarding to a customer."
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a98f489-New_Reward_Item_-_Set_PrizeOut_Point_1.png",
        "New Reward Item - Set PrizeOut Point (1).png",
        1440,
        901,
        "#000000"
      ]
    }
  ]
}
[/block]
5. Click **Create** to submit all inputs.
[block:api-header]
{
  "title": "Using monetization-enabled reward item for an action"
}
[/block]
Now you have successfully created a new reward item with the Prizeout feature and now let’s see how to use that.


1. Navigate to **Rewards** > **Tables**. Then Create a new reward table or click on an existing table.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/54f2191-Reward_table.png",
        "Reward table.png",
        1440,
        900,
        "#000000"
      ]
    }
  ]
}
[/block]
2. Click **New Entry** to create a reward for an action.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/403ae96-Reward_table_entries.png",
        "Reward table entries.png",
        1440,
        901,
        "#000000"
      ]
    }
  ]
}
[/block]
3. Select an action from the **Reward Action** Dropdown.
4. Select an item from the **Reward Item** dropdown for which you added the conversion rate in the reward item creation step.
5. Enter an amount in the **Reward Amount** input field and that amount will be received by the users.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4edd928-Reward_table_entries_-_New.png",
        "Reward table entries - New.png",
        1440,
        900,
        "#000000"
      ]
    }
  ]
}
[/block]
For example, as you can see above that once a customer performs a “Vote on a poll” action, he will receive 500 “LiveLike Points” which is equal to "5 Prizeout Points“.



7. Click **Create** to submit all inputs.


After all of these steps, you have successfully created a reward item with prizeout feature. Now, you can move forward with client side integration to let your users earn prizeout points each time when they earn this item and redeem gift cards. 
[block:api-header]
{
  "title": "Client Side Integration"
}
[/block]
Before loading the Prizeout marketplace widget on the client side, you will need to create Prizeout User Session using the [API Endpoint](https://docs.livelike.com/reference/prizeout-user-session) provided by LiveLike.
Use the `session_id` to initialise the Prizeout SDK. 

Refer [Prizeout API documentation](https://partners.prizeout.com/#/api) for more details.

Below is an example of how you can integrate prizeout and let users redeem gift cards with their prizeout points. Follow the steps mentioned above and fill in all the required keys in the config.js file.
[block:embed]
{
  "html": false,
  "url": "https://stackblitz.com/edit/js-yznhaz?file=index.html,config.js,index.js,style.css",
  "title": "Prizeout Integration - StackBlitz",
  "favicon": "https://c.staticblitz.com/assets/favicon-editor-675989317f34707a17fe9d649da3609d70f6f8abc9546445389238ddd570a1d4.png",
  "image": "https://social-img.staticblitz.com/projects/js-yznhaz/05753624e44b6fe5d970c1878ba50536",
  "iframe": true
}
[/block]