---
title: WidgetModel
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: WidgetModel | Flutter SDK | LiveLike Developer Hub
  description: >-
    WidgetModel is the data layer class that allows the integrator to use the
    APIs of LiveLike associated widgets. Learn more.
  robots: index
next:
  description: ''
---
WidgetModel is the data layer class that allows the integrator to use the APIs of LiveLike associated widgets.
[block:api-header]
{
  "title": "Create WidgetModel"
}
[/block]
In Order to create the widget Model 

**Create using LiveLikeWidget Model class:** 

[block:code]
{
  "codes": [
    {
      "code": "   final widgetModel = await session.fetchWidgetModel(<LiveLikeWidget class instance>);",
      "language": "text",
      "name": "Dart"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "WidgetModel"
}
[/block]
Components of WidgetModel:

**LiveLikeWidget**
The instance of the livelikeWidget class which is used to create the widget model, contains the data of the widgets

**Vote Api** 
In Order to vote on a particular option, the voting method is used, it contains optionId and magnitude , magnitude is used for sending vote for Image Slider Widget, and for the rest of the widget the optionId is sent.


[block:code]
{
  "codes": [
    {
      "code": "widgetModel.vote(magnitude: <value>);\nwidgetModel.vote(optionId: <value>)",
      "language": "text",
      "name": "Dart"
    }
  ]
}
[/block]
**Vote Result Stream** 
In Order to receive the vote count for options associated with a widget, the voteResultStream is used. It returns the instance of VoteCountResult class, which contains the option id,vote count,magnitude values
[block:code]
{
  "codes": [
    {
      "code": "widgetModel?.voteCountResultStream.listen((event) {\n//VoteCountResult\n}))",
      "language": "text",
      "name": "Dart"
    }
  ]
}
[/block]
**Dispose** 

The dispose method is used to clear and release the instances associated to widgetModel.
[block:code]
{
  "codes": [
    {
      "code": "widgetModel.dispose()",
      "language": "text",
      "name": "Dart"
    }
  ]
}
[/block]