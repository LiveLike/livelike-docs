---
title: Widget Impressions
excerpt: Track widget viewers
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Widget impressions are tracked automatically when using a LiveLike SDK integration.  However, when using a REST API integration they will have to be tracked manually.  Every widget resource in the REST API has an `impression_url` field.  Submit an HTTP POST request to this URL with an empty request body, and the user's Profile Access Token to register an impression.

```python
# Fetch the widget data
r = requests.get("https://cf-blast.livelikecdn.com/api/v1/alerts/1bb8738a-66fc-4aeb-ae0a-0f0a5cffae01/")
r.raise_for_status()
widget_data = r.json()

# Register an impression on the widget:
impression_url = widget_data["impression_url"]
r = requests.post(impression_url, headers={"Authorization": f"Bearer {profile_access_token}"})
r.raise_for_status()
```
