---
title: Create a Poll Vote
excerpt: ''
api:
  file: engagement-suite.json
  operationId: create-poll-vote
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
When a Poll widget is created, an array of `options` is part of the data. Each of these options include an `id` and a `vote_url`, among other fields. 

Voting on a Poll can be accomplished two ways:

1. Make a POST request to this `vote_url` field. 
2. Make a POST request to the above endpoint.

Once that request is made, the option's `vote_count` field will be incremented by 1.

This request requires a user profile's `access_token` to be sent as the Bearer Token in the requests authorization headers. This is what associates the widget interaction with the user profile. Once this request is made, the widget interaction is created, and can be viewed through the [widget interaction endpoint](https://docs.livelike.com/reference/get-widget-interactions) .

If the widget is connected to a [Reward Item](https://docs.livelike.com/docs/rewards) , once the request is made the user is rewarded, and the reward can be viewed through the [Reward Transaction endpoint](https://docs.livelike.com/reference/list-reward-transactions) .