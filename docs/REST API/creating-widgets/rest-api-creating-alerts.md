---
title: Creating Alerts
excerpt: How to create alert widgets with the REST API
deprecated: false
hidden: false
metadata:
  title: Creating Alerts | REST API | LiveLike Developer Hub
  description: >-
    Alerts are a quick and versatile way to interact with your audience. Learn
    how to create alerts with our REST APIs.
  robots: index
next:
  description: ''
  pages:
    - type: link
      title: Alert Widgets Guide
      url: https://docs.livelike.com/docs/widgets#section-alerts
    - type: link
      title: Using Widgets in the REST API
      url: https://docs.livelike.com/v1/reference#widgets-basics
---
Alerts are a quick and versatile way to interact with your audience. They can contain text only, an image only, or a combination of both. Links can also be attached so that they can act as a call-to-action for your audience. For more details, see the [Alerts product guide](doc:widgets#section-alerts).

## Create an Alert

All widgets are created as part of a <Glossary>Program</Glossary> and each program has its own unique ID. To send an alert widget, a new alert must first be created within the program that your audience will be interacting with. Here is a simple "Hello world!" text-only alert:

```python
# Configure your Program ID
program_id = "your-program-id"

# Set up authorization headers using your API access token
headers = {'Authorization': f'Bearer {access_token}'} 
           
# Create a new text-only alert widget
payload = {'program_id': program_id, 'text': 'Hello world!'}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/alerts/', json=payload, headers=headers)
alert = r.json()
```

Once a widget is created, it will appear in the Pending section of the Producer Studio, but users won't see it yet. A widget has to be published before an audience will see it.

> 📘 More info is in the API reference!
>
> Please see the [Using Widgets](https://docs.livelike.com/v1/reference#widgets-basics) section of the API reference documentation for more details about how widgets are created and published.

## Publish the Alert

Widgets get published according to the program schedule. Every widget has a `schedule_url` field that can be called to update the schedule. The schedule works by setting a delay on a widget, and once the delay is reached the widget gets published. If you want to publish a widget immediately, use a delay of zero. Here is how you would immediately publish the alert created earlier:

```python
# Schedule the alert to publish immediately
publish_payload = {'publish_delay': 'P0DT0S'}
requests.put(alert['schedule_url'], json=publish_payload, headers=headers)
```

> 👍 Specify publish delays in ISO format
>
> The `publish_delay` body parameter is specified in ISO 8601 duration format.

Once the alert is published, it will appear in the History tab in the Producer Studio, and audiences will see it on their devices if they are subscribed to the program.

## Alert Variations

The alert widget supports a few variations. The variation to use is decided when the widget is created. These variations include:

* Text-only, by specifying only the `text` field
* Image-only, by specifying only the `image_url` field
* Text and image, by specifying both the `text` and `image_url` fields

Links can also be attached to alerts by specifying the `link_label` and `link_url` fields when creating them.
