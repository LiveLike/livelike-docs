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

> 🚧 Web SDK version 1.8 required

## Example

As a first example, we will add a `results` event listener that plays an animation when someone gets a quiz correct:

```javascript example.js
const widgets = document.getElementById('widgets')

widgets.addEventListener('results', function (ev) {
  switch (ev.target.widgetPayload.kind) {
    case 'text-quiz':
    case 'image-quiz':
      if (ev.detail.result === 'correct') {
        playCorrectQuizResultAnimation() // Not provided by SDK
      }
      break
  }
})
```
```html example.html
<livelike-widgets id="widgets" programid={programid}></livelike-widgets>
```

This works because the quiz widgets emit a `results` event when the correct answer is revealed. If the user was correct, it plays a custom animation not provided by the SDK.

## Supported Widgets

The Text Quiz, Image Quiz, Text Prediction Follow-up, and Image Prediction Follow-up widgets fire events that allow developers to customize the feedback to correct and incorrect answers. The exact list of widget kinds are:

* `text-quiz`
* `image-quiz`
* `text-prediction-follow-up`
* `image-prediction-follow-up`

## The Results Event

The `results` event has a `detail` property containing the result of the user's interaction with the widget. The detail object contains a single property named `result` that will be either `"correct"` or `"incorrect"`. The results event will not fire if the user did not interact with the widget.
