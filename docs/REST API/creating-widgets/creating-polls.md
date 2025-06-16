---
title: Creating Polls
excerpt: How to create poll widgets with the REST API
deprecated: false
hidden: false
metadata:
  title: Creating Polls | REST API | LiveLike Developer Hub
  description: >-
    Polls ask your audience to let everyone know how they feel or what they
    think. Learn how to create polls with our REST APIs.
  robots: index
next:
  description: ''
---
Polls ask your audience to let everyone know how they feel or what they think. The REST API has two types of polls: text variants and image variants. A poll is made up a question and a list of options. Options are limited from 2–4 entries. Image polls must have an image associated with each option.

## Create a Poll

All widgets are created as part of a <<glossary:Program>> and each program has its own unique ID. To send a poll widget, a new one must first be created within the program that your audience will be interacting with. When creating a poll, the `program_id`, `question`, and `options` body parameters are required.

```python createimagepoll.py
# Configure your Program ID
program_id = "your-program-id"

# Set up authorization headers using your API access token
headers = {'Authorization': f'Bearer {access_token}'} 
           
# Create a new image poll  widget
payload = {
  'program_id': program_id,
  'question': "Is this Eli's last game with the giants?",
  'options': [
    {
      'image_url': 'https://example.com/yes.png',
      'description': "For sure! He's done."
    },
    {
      'image_url': 'https://example.com/no.png',
      'description': "He still has a lot left in the tank!"
    }
  ]
}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/image-polls/', json=payload, headers=headers)
poll = r.json()
```

Once a widget is created, it will appear in the Pending section of the Producer Studio, but users won't see it yet. A widget has to be published before an audience will see it.

> 📘 Check out Polls API reference
> 
> More details on [reading polls](https://docs.livelike.com/reference#get-an-image-poll) and [creating polls](https://docs.livelike.com/reference#create-image-poll) is available in the API reference.

## Publish the Poll

Widgets get published according to the program schedule. Every widget has a `schedule_url` field that can be called to update the schedule. The schedule works by setting a delay on a widget, and once the delay is reached the widget gets published. If you want to publish a widget immediately, use a delay of zero. Here is how you would immediately publish the widget created earlier:

```python
# Schedule the widget to publish immediately
publish_payload = {'publish_delay': 'P0DT0S'}
requests.put(poll['schedule_url'], json=publish_payload, headers=headers)
```

> 👍 Specify publish delays in ISO format
> 
> The `publish_delay` body parameter is specified in ISO 8601 duration format.

Once the widget is published, it will appear in the History tab in the Producer Studio, and audiences will see it on their devices if they are subscribed to the program.

> 📘 More info is in the API reference!
> 
> Please see the [Using Widgets](https://docs.livelike.com/v1/reference#widgets-basics) section of the API reference documentation for more details about how widgets are created and published.

## Poll Variations

The REST API supports two poll variants, text polls and image polls. They function mostly identically, except for these key differences:

- Image poll and text poll are two separate API resources
- Image poll options require an `image_url` field that text poll options do not have