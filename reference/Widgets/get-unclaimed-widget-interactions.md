---
title: Get Unclaimed Widget Interactions
excerpt: ''
api:
  file: profiles.json
  operationId: get-unclaimed-widget-interactions
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The `claim_token` is used to claim rewards from Prediction widgets. To claim the reward, make a `post` request to the Prediction Follow Up widget's `claim_url` field. The response will include the `rewards` array. 

The Prediction Follow Up resource can be fetched directly by making a `get` request to the prediction Follow Up widget's `url` field.

Using the `Unclaimed Widget Interaction` response above, you can make a get request to Prediction widget, and access the Prediction Follow Up `claim_url` from within the Prediction resource.
[block:code]
{
  "codes": [
    {
      "code": "import requests\n\nprediction_response = requests.get('https://cf-blast.livelikecdn.com/api/v1/text-predictions/509677e0-b40a-4d29-8c8b-e29f017f7e0c/')\nprediction = prediction_response.json()\nfollow_up = prediction['follow_ups'][0]\n\nclaim_response = requests.post(follow_up['claim_url'])\nclaim = claim_response.json()\nrewards = claim['rewards']",
      "language": "python"
    }
  ]
}
[/block]