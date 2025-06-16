---
title: Prizeout
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    You will successfully integrate Prizeout with LiveLike after completing all
    the above steps. The next step is to set up Prizeout for monetization
    feature in a reward item. Please read this documentation to set up Prizeout
    in rewards.
  pages:
    - type: basic
      slug: prizeout-for-rewards
      title: Prizeout for Rewards
---
Integrating Prizeout with LiveLike CMS enables the points redemption feature in your platform to engage your customers with an exciting gamification experience. to know more about this feature please check <a href="https://docs.livelike.com/docs/prizeout-for-rewards" target="_blank">here</a> this out.
[block:api-header]
{
  "title": "How to connect Prizeout to LiveLike?"
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "Make sure you have an account with Prizeout and have access to their partner dashboard. If you don't have one please create one from <a href=\"https://partners.prizeout.com/#/register\" target=\"_blank\">here</a>.",
  "title": "Make sure you have an account with Prizeout"
}
[/block]
We have made enabling this feature very easy for you and please follow the below steps in LiveLike CMS for integration.

1. Navigate to **Integrations** then look for Prizeout and click **Connect** button to start integrating.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0798e4c-PO-integration.png",
        "PO-integration.png",
        1440,
        900,
        "#000000"
      ],
      "caption": ""
    }
  ]
}
[/block]
2. Enter Prizeout **Partner ID, API Key, API Secret Key,** and **HTTP Security Token** in respective input fields
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d733492-PO-keys.png",
        "PO-keys.png",
        1440,
        900,
        "#000000"
      ]
    }
  ]
}
[/block]
To get all the required fields, Go to Prizeout dashboard and navigate **Prizeout Dashboard** > **Account Settings**

3. Click **Connect** button to complete integration.


4. Once the integration is successful then you will see an **Active** switch is on.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a463ed0-PO-active.png",
        "PO-active.png",
        1440,
        900,
        "#000000"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Callback APIs"
}
[/block]
Prizeout calls a series of HTTP callbacks provided by LiveLike to trigger some actions like verifying user balance. Following are the APIs which you need to paste in your **Prizeout Dashboard** > **Account Settings** with each relevant label.
[block:parameters]
{
  "data": {
    "h-0": "Label",
    "h-1": "Description",
    "h-2": "API Endpoint",
    "0-0": "Balance Check",
    "1-0": "Cashout Success",
    "2-0": "Cashout Fail",
    "3-0": "Session",
    "0-1": "Used to verify the user's balance",
    "1-1": "Executed when a cash out request is completed and successful.",
    "2-1": "Executed when a cash out request fails.",
    "3-1": "Prizeout will ask at various stages if the session_id you passed us is valid.",
    "0-2": "https://cf-blast.livelikecdn.com/api/v1/applications/{client_id}/prizeout-callback-balance/",
    "1-2": "https://cf-blast.livelikecdn.com/api/v1/applications/{client_id}/prizeout-callback-success/",
    "2-2": "https://cf-blast.livelikecdn.com/api/v1/applications/{client_id}/prizeout-callback-failure/",
    "3-2": "https://cf-blast.livelikecdn.com/api/v1/applications/{client_id}/prizeout-callback-session/"
  },
  "cols": 3,
  "rows": 4
}
[/block]