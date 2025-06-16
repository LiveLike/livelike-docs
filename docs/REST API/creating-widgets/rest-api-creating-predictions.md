---
title: Creating Predictions
excerpt: How to create prediction widgets with the REST API
deprecated: false
hidden: false
metadata:
  title: Creating Predictions | REST API | LiveLike Developer Hub
  description: >-
    The REST API has text predictions and image predictions. Learn how to create
    prediction widgets with the REST API.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: attaching-custom-data-to-widgets
      title: Attaching Custom Data to Widgets
---
This guide is for server-side developers who want to automate publishing predictions for their audience. These same tools are available in the Producer Site for a human operator to use, but this guide focuses on the automation use-case such as creating a data-driven predictions game. See the [widgets guide section on predictions](doc:widgets#predictions) for general information about the prediction widget. 

Predictions are a two-step interaction. In the first step, the prediction, the audience is asked a question for which the answer is not yet known and are given a set of options to choose from. In the second step, the follows-up reveals which of the options was correct.

The REST API has two types of predictions: text predictions and image predictions. A prediction is made up a question and a list of options. Predictions are limited from 2–4 options, any or all or none of which may turn out to be be correct. Image predictions must have an image associated with each choice.

## Create a Prediction

All widgets are created as part of a <<glossary:Program>> and each program has its own unique ID. To send a prediction widget, a new one must first be created within the program that your audience will be interacting with. When creating a prediction, the `program_id`, `question`, and `options` body parameters are required.

```python createimageprediction.py
# Configure your Program ID
program_id = "your-program-id"

# Set up authorization headers using your API access token
headers = {'Authorization': f'Bearer {access_token}'} 
           
# Create a new image prediction widget
payload = {
  'program_id': program_id,
  'question': 'Will Patrick M. throw more than 4 touchdown passes today?',
  'options': [
    {
      'image_url': 'https://example.com/image1.png',
      'description': 'Yes. Today is going to be an air show!'
    },
    {
      'image_url': 'https://example.com/image2.png',
      'description': "No. Broncos defense is too good!"
    }
  ]
}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/image-predictions/', json=payload, headers=headers)
prediction = r.json()
```

Once a prediction is created, two widgets will appear in the Pending section of the Producer Studio, but users won't see either of them yet. The two widgets are:

- The prediction widget. Once published, the audience will be able to guess which option will be correct.
- The follow-up widget. Once published, the audience will find out which options were correct.

> 🚧 Users don't see the prediction yet!
> 
> The widget is created, and it's pending in the queue, but it hasn't yet been published.

> 📘 More info is in the API reference!
> 
> Please see the [Using Widgets](https://docs.livelike.com/v1/reference#widgets-basics) section of the API reference documentation for more details about how widgets are created and published.

## Publish the Prediction

Widgets get published according to the program schedule. Every widget has a `schedule_url` field that can be called to update the schedule. The schedule works by setting a delay on a widget, and once the delay is reached the widget gets published. If you want to publish a widget immediately, use a delay of zero.

Once you are ready to accept guesses from the audience, here is how you would immediately publish the prediction created earlier:

```python
# Schedule the prediction to publish immediately
publish_payload = {'publish_delay': 'P0DT0S'}
requests.put(prediction['schedule_url'], json=publish_payload, headers=headers)
```

> 👍 Specify publish delays in ISO format
> 
> The `publish_delay` body parameter is specified in ISO 8601 duration format.

Once the widget is published, it will appear in the History tab in the Producer Studio, and audiences will see it on their devices if they are subscribed to the program. The interaction isn't complete yet though, the audience still has to wait for the follow-up to know if they were right or not.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0f33478-95fa43e-image_poll_7.gif",
        "95fa43e-image_poll_7.gif",
        1422
      ],
      "align": "center",
      "caption": "Users will see the prediction once it's published."
    }
  ]
}
[/block]


## Update the Correct Options

Once you know which of the options is correct, modify the resource of each correct option to set its `is_correct` field to `true`.

```python
# Let's assume the first option was correct
follow_up = prediction['follow_ups'][0]
option = follow_up['options'][0]

# Mark the first option as correct
update_payload = {'is_correct': True}
requests.patch(option['url'], payload=update_payload, headers=headers)
```

## Publish the Follow-up

Once all of the correct options have been marked, the follow-up can be published:

```python
# Schedule the follow-up to publish immediately
publish_payload = {'publish_delay': 'P0DT0S'}
requests.put(follow_up['schedule_url'], json=publish_payload, headers=headers)
```

## Prediction Variations

The REST API supports two prediction variants, text predictions and image predictions. They function mostly identically, except for these key differences:

- Image prediction and text predictions are two separate API resources
- Image prediction options require an `image_url` field that text prediction options do not have