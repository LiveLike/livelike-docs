---
title: Widget UI Lifecycle
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
Widget when rendered could be in different phases based on its kind. Lets first understand what are single interaction, multi interaction and follow up based widgets.

#### Single interaction:

Such widget kind would be interacted only once by user, usually such widget kinds would have submittable type of UI where after submission, widget gets into disabled state permanently, Widget Kind Eg:

* Text or Image Quiz
* Number Prediction
* Emoji Slider
* Text Ask

#### Multi interaction:

Such widget could be interacted multiple times until widget interactivity is timed out or expired. Widget Kind Eg:

* Text or Image Poll
* Text or Image Prediction
* Cheer Meter

#### Follow up:

Follow up widgets are are always non interact-able widgets that shows result of the prediction widget i.e text/image prediction or number prediction widget. Whenever a follow up is published, a prediction widget gets into `FOLLOWUP_PUBLISHED` Phase where it gets into disabled state.

let us try to understand widget UI lifecycle using below scenarios:

##### Scenario 1:

*Considering a scenario where widget is rendered for the very first time and user interacts with the widget (and presses submit button).*

![](https://files.readme.io/1d51c21-Initial_3.svg)

* After a user interacts with the widgets (and presses submit button), widget gets into Submitting phase where interaction request is been submitted to our widget service. This is inflight request UI state so usually observed for a short span of time.
* Once the Interaction response is received from widget service, widget transitions into `Submitted` phase where single interaction based widget gets permanently into disabled state and multi interaction based widget again transition back to `Interactive`.

##### Scenario 2:

*Considering a scenario where your UI is reloaded and widget rendered already has user interaction.*

![](https://files.readme.io/7737c69-ReloadUI.svg)

* Single Interaction based widget are rendered in Submitted phase where UI is in disabled state
* Multi Interaction based widget follows usual lifecycle of Interactive -> Submitting -> Interactive

##### Scenario 3:

*Considering a scenario where widget is rendered with a given interactivity time out or expiry date time and user does not interacts with the widget.*

![](https://files.readme.io/b5bff1c-EndPhase_3.svg)

* Interactivity timeout if present starts once the widget gets rendered. After the interactivity times out, widget gets into `Timeout`Phase where it is in disabled state. (Interactive timeout is set from producer suite when creating a widget) 
* Widget expiry if present checks if the current date time is less than expiry time. In the case current date time exceeds expiry date time, then widget gets into `Expired`Phase where it is in disabled state. (Expiry date time is set from producer suite when creating a widget).
