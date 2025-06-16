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
All widgets are created as part of a <<glossary:Program>>. A widget that was published to one program cannot be published to another one.
[block:callout]
{
  "type": "info",
  "title": "One program per video in your app",
  "body": "It is generally a good idea to have a program for each video in your app. That way it is easier for producers to stay organized with what is live now and what is coming up next, and it is also easier to go back in the history and review analytics and metrics for a specific video."
}
[/block]

[block:api-header]
{
  "title": "Get Widgets for Program"
}
[/block]
Once a widget has been created in a program it is available in the API. Each program has a `widgets_url` hyperlink field that can be requested to get all the widgets created in that program. The program widgets resource is paginated.
[block:code]
{
  "codes": [
    {
      "code": "import requests\n\n# Fetch program resource\nr = requests.get('https://cf-blast.livelikecdn.com/api/v1/programs/f1938a34-2611-4cff-9043-ad6b3dd2f6fd/')\nprogram = r.json()\n\n# Fetch program's widget history using the widgets_url\nr = requests.get(program['widgets_url'])\nhistory = r.json()",
      "language": "python"
    }
  ]
}
[/block]