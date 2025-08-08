---
title: Using Programs
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
All widgets are created as part of a <Glossary>Program</Glossary>. A widget that was published to one program cannot be published to another one.

> 📘 One program per video in your app
>
> It is generally a good idea to have a program for each video in your app. That way it is easier for producers to stay organized with what is live now and what is coming up next, and it is also easier to go back in the history and review analytics and metrics for a specific video.

## Get Widgets for Program

Once a widget has been created in a program it is available in the API. Each program has a `widgets_url` hyperlink field that can be requested to get all the widgets created in that program. The program widgets resource is paginated.

```python
import requests

# Fetch program resource
r = requests.get('https://cf-blast.livelikecdn.com/api/v1/programs/f1938a34-2611-4cff-9043-ad6b3dd2f6fd/')
program = r.json()

# Fetch program's widget history using the widgets_url
r = requests.get(program['widgets_url'])
history = r.json()
```

## Start or Stop Program

```python Python
import requests

# Set up authorization headers using a producer access token
headers = {'Authorization': f'Bearer {access_token}'} 

# Fetch program resource
r = requests.get('https://cf-blast.livelikecdn.com/api/v1/programs/f1938a34-2611-4cff-9043-ad6b3dd2f6fd/')
program = r.json()

# Start the program
requests.post(program['start_program_url'], headers=headers)

# Stop the program
requests.post(program['stop_program_url'], headers=headers)
```