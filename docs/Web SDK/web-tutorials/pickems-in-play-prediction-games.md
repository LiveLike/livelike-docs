---
title: Pick'ems & In Play Prediction games
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Pick'ems & In Play Prediction Games | Web SDK | LiveLike
  description: >-
    Check out this tutorial to learn how to use LiveLike's widget APIs to build
    Pick'ems & In Play Prediction games.
  robots: index
next:
  description: ''
---
In this tutorial we will use LiveLike's widget APIs to build Pick'ems & In Play Prediction games
[block:api-header]
{
  "title": "The Idea"
}
[/block]
**Pick 'em game**: batches of predictions are made at regular intervals either before or during a game

**In-play predictions games**: predictions are continuously made throughout a live event


We will build In-play predictions games by creating custom widget timeline using `getWidgets` method which will show only predictions (with no timer)

Integrators can also modify this code to create Pick 'em game by filtering with widget IDs
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/tanyalivelike/embed/XWebjYg' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/tanyalivelike/pen/XWebjYg",
  "title": "Prediction Games",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico"
}
[/block]