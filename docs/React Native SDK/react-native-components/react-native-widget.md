---
title: Widget
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
The various interactive elements that are delivered to audiences to engage with are called widgets. The library of widgets is always expanding and features things like polls, quizzes, and predictions.

> 📘 What are widgets, different available widgets and presentational modes?
> 
> Refer our [widget](https://docs.livelike.com/docs/widgets) core documentation

> 📘 Widget core concepts
> 
> As a pre-requisite we recommend you to go through our widget core concepts documentation that would help you to understand below different widgets, their structure and available customisations.
> 
> [Widget Anatomy](react-native-widget-anatomy) 
> 
> [Widget UI Lifecycle](react-native-widget-ui-lifecycle)

> 👍 Snack expo playground
> 
> Refer [livelike-widgets](https://snack.expo.dev/@aquibv/livelike-widgets) snack expo playground

React Native SDK provides different stock widget UI components:

1. [LLPollWidget](react-native-llpollwidget) - Poll option based widget that could be either text or image based on `widgetKind`
2. [LLQuizWidget](react-native-llquizwidget) - Quiz choice based widget that could be either text or image based on `widgetKind`
3. [LLPredictionWidget](react-native-llpredictionwidget) - Prediction based widget that could be either text or image based on `widgetKind`. Every prediction based widget has a follow up widget that shows the user actual result of the prediction. For example a prediction widget which lets user to predict the winner of the football match, a follow up widget would show the actual winner along with the overall vote counts.
4. [LLPredictionFollowUpWidget](react-native-llpredictionfollowupwidget) - Prediction follow up widget that could be either text or image based on `widgetKind`. This widget is always a non interact-able widget.
5. [LLNumberPredictionWidget](react-native-llnumberpredictionwidget) - Number prediction based widget that could be either text or image based on `widgetKind`.
6. [LLNumberPredictionFollowUpWidget](react-native-llnumberpredictionfollowupwidget) - Number prediction based widget that could be either text or image based on `widgetKind`. Number prediction widget lets user prediction
7. [LLEmojiSliderWidget](react-native-llemojisliderwidget) - Slider based widget that could have different emojis presented at different sliding levels.
8. [LLCheerMeterWidget](react-native-llcheermeterwidget) - Cheer meter based widget that could empower user to cheer for their teams, player , etc.