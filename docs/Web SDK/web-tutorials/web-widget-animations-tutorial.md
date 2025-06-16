---
title: Widget Animations Tutorial
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Animations Tutorial | Web SDK | LiveLike
  description: >-
    Some widgets fire events after a user interacts with them, allowing
    developers to add custom feedback depending on the user's interaction.
  robots: index
next:
  description: ''
---
Some widgets fire events after a user interacts with them, giving developers the opportunity to add custom feedback depending on the user's interaction.
[block:callout]
{
  "type": "warning",
  "title": "Web SDK version 1.8 required"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Example"
}
[/block]
As a first example, we will add a `results` event listener that plays an animation when someone gets a quiz correct:
[block:code]
{
  "codes": [
    {
      "code": "const widgets = document.getElementById('widgets')\n\nwidgets.addEventListener('results', function (ev) {\n  switch (ev.target.widgetPayload.kind) {\n    case 'text-quiz':\n    case 'image-quiz':\n      if (ev.detail.result === 'correct') {\n        playCorrectQuizResultAnimation() // Not provided by SDK\n      }\n      break\n  }\n})",
      "language": "javascript",
      "name": "example.js"
    },
    {
      "code": "<livelike-widgets id=\"widgets\" programid={programid}></livelike-widgets>",
      "language": "html",
      "name": "example.html"
    }
  ]
}
[/block]
This works because the quiz widgets emit a `results` event when the correct answer is revealed. If the user was correct, it plays a custom animation not provided by the SDK.
[block:api-header]
{
  "title": "Supported Widgets"
}
[/block]
The Text Quiz, Image Quiz, Text Prediction Follow-up, and Image Prediction Follow-up widgets fire events that allow developers to customize the feedback to correct and incorrect answers. The exact list of widget kinds are:

* `text-quiz`
* `image-quiz`
* `text-prediction-follow-up`
* `image-prediction-follow-up`
[block:api-header]
{
  "title": "The Results Event"
}
[/block]
The `results` event has a `detail` property containing the result of the user's interaction with the widget. The detail object contains a single property named `result` that will be either `"correct"` or `"incorrect"`. The results event will not fire if the user did not interact with the widget.