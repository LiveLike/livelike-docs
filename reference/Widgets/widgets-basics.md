---
title: Using Widgets
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
Developers have fine control over the lifecycle of a widget. Widgets are sent to audiences in two steps: first they are created, and then they are published. This allows for complex workflows to be managed, so that widgets can be created, edited, scheduled, etc. ahead of time before publishing.

When a widget is published, its payload is delivered over PubNub so that subscribed clients can show it live without having to poll the program timeline API.

## Creating Widgets

When a widget is first created, it is considered *pending*. It exists in the system and can be referenced in the API, but has not been published to an audience. Here is some sample code for creating an alert widget:

```python
import requests

payload = {'program_id': program_id, 'text': 'Hello world!'}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/alerts/', json=payload)
```

This widget hasn't been delivered to audiences yet, but it has been created and will appear in the Pending tab inside the Producer Studio. A producer can now post it and send it out to the audience, or schedule it for later.

## Updating Widgets

When a widget is created, the response contains a `url` field. This is the url of the widget resource. A patch request can be made to this url to update fields in the payload used to create the widget.

```python
import requests

payload = {'program_id': program_id, 'text': 'Hello world!'}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/alerts/', json=payload)
alert = r.json()

update = {'text': 'Updated Hello world!'}
requests.patch(alert['url'], json=update)
```

## Publishing Widgets

A pending widget has to be *scheduled* for it to be published. All publication is done through scheduling, and posting a widget immediately is semantically equivalent to scheduling for now. Widgets can also be scheduled for publishing in the future by scheduling with a delay. Every widget has an associated `schedule_url` field that must be called with a `publish_delay` in ISO duration format to schedule it.

Here's how an alert would be immediately published:

```python
import requests

# Create a new alert widget
payload = {'program_id': program_id, 'text': 'Hello world!'}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/alerts/', json=payload)
alert = r.json()

# Schedule the alert to publish immediately
requests.put(alert['schedule_url'], json={'publish_delay': 'P0DT0S'})
```

Scheduled widgets will appear in the Scheduled tab in the Producer Studio. Once the delay is reached, the widget will be published and sent to the audience. Widgets can be scheduled to post in the future. Here is how that alert created earlier would be scheduled to publish an hour from after the request is made:

```python
# Schedule the alert to publish in one hour
requests.put(alert['schedule_url'], json={'publish_delay': 'P0DT1H'})
```

Scheduled widgets can be unscheduled and revert to pending. Removing a schedule time from a widget is done by issuing a DELETE request to its `schedule_url`.

```python
# Un-schedule the alert
requests.delete(alert['schedule_url'])
```
