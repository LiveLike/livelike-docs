---
title: Building Custom Widget UI
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Minimum SDK Version
>
> iOS: 2.11
> Android: 2.8
> Web: 2.0.0

Although the EngagementSDK offers high-fidelity widget UI which provide engaging experiences for your users, you may want to implement you own UI to match your applications particular use-case or aesthetic. We provide methods for you to go above and beyond small cosmetic changes possible with the Theme system and fundamentally change how user's will engage with a widget.

Its as easy as

1. Build your Widget UI
2. Access the Widget data
3. Connecting your UI to the Widget Data

**Platform Docs**
[iOS](doc:accessing-widget-data)
[Android](doc:livelikewidgetviewfactory)
[Web](doc:widget-configuration)

**Sample Application**
[Android](https://github.com/LiveLike/SampleAndroidApp)

## Accessing Widget Data

There are 3 channels in which Widget data can be accessed. Choose the one that best fits your use-case.

1. Realtime Widgets - The widgets that are published by a Producer
2. On Demand By ID - Load a widget from the server by it's id
3. On Demand From History - Loads a page of widgets from the publish history

## Building a Cheer Meter Widget

A Cheer Meter Widget is a fast-paced and high-action widget to allow fans to express their emotion.

**Platform Docs**
[iOS Tutorial](doc:building-a-cheer-meter-widget-2)
[Android](doc:building-a-cheer-meter-widget-1)
[Web](doc:custom-widget-examples#cheer-meter-widget)

## Building an Alert Widget

An Alert Widget is an informational widget to share news, updates, and promotional content.

**Platform Docs**
[iOS Tutorial](doc:building-an-alert-widget)
[Android](doc:building-a-alert-widget)
[Web](doc:custom-widget-examples#alert-widget)

## Building a Quiz Widget

A Quiz Widget is trivia type widget where user's can flex their knowledge! A user can only have one answer per Quiz.

**Platform Docs**
[iOS API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/QuizWidgetModel.html)
[Android](doc:building-a-quiz-widget-1)
[Web](doc:custom-widget-examples#quiz-widget)

## Building a Poll Widget

A Poll Widget is a widget where user's can share opinions and compare with other's.

**Platform Docs**
[iOS API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/PollWidgetModel.html)
[Android](doc:building-a-poll-widget-1)
[Web](https://docs.livelike.com/docs/custom-widget-examples#poll-widget)

## Building a Prediction

A Prediction is composed of two Widget types. The Prediction Widget itself and the Prediction Follow Up Widget.

**Platform Docs**
[iOS Prediction API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Protocols/PredictionWidgetModelDelegate.html)
[iOS Prediction Follow Up API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/PredictionFollowUpWidgetModel.html)
[Android](https://docs.livelike.com/docs/building-a-prediction-and-followup-widget)
[Web](https://docs.livelike.com/docs/custom-widget-examples#prediction-widget)

## Building a Text Ask Widget

Ask widget is basically used to collect audiences replies and feature the best one.

**Platform Docs**
[iOS API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/TextAskWidgetModel.html)
[Android](https://docs.livelike.com/docs/building-a-text-ask-widget)
[Web](https://docs.livelike.com/docs/custom-widget-examples#text-ask-widget)

## Building a Number Prediction Widget

Number Prediction widgets allows your audience to make predictions as numbers so that you can ask about things like sports scores, player performance, number of seconds in a national anthem, etc.

**Platform Docs**
[Android](https://docs.livelike.com/docs/building-a-number-prediction-and-followup-widget)
[Web] ([https://docs.livelike.com/docs/custom-widget-examples#number-prediction-widget](https://docs.livelike.com/docs/custom-widget-examples#number-prediction-widget))
