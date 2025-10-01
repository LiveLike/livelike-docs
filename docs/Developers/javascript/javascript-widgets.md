---
title: Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-chat
      title: Chat
---
The various interactive elements like polls, quizzes, and predictions are called widgets. A list of the available widgets can be found in the [widgets product guide](doc:widgets).\
This section details all the widget based API exported as part of Javascript package.

## Real Time published widgets

To get widget details published from producer suite in real time, refer [`addProgramListener`](javascript-program) API. 

## getPostedWidgets

This API can be used to get published widgets for the program. It takes a required `programId` argument object property.

**API Definition:** [getPostedWidgets](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getPostedWidgets)

```javascript
import { getPostedWidgets } from '@livelike/javascript';

getPostedWidgets({
  programId: "*****",
  // option widget attributes to get widgets based on certain attributes
  widgetAttributes: [ {key: "fruit", value: "apple"} ]
}).then(res =>  console.log('res', res));
```

## getWidgetsInteractions

This API can be used to get interactions for the user for a given set of widgets or for the interactionUrl returned form the timeline resource.\
It takes an interactionUrl, or a programId and an array of widget's kind and id.

**API Definition:** [getWidgetsInteractions](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getWidgetsInteractions)

> 🚧 No Interactions for follow up widgets
>
> For followup widgets, there are no interaction. They should be attached with the interaction on their corresponding non followup widget.

```javascript
import { getWidgetsInteractions, WidgetKind } from '@livelike/javascript';

getWidgetsInteractions({
  programId: "*****",
  widgets: [{ kind: WidgetKind.CHEER_METER, id:"*****"}]
})
```

## getWidgetInteractions

This API gives you widget interactions for a given widget.\
Only in the case of Cheer meter widget, widget interaction would be list of more than one interaction element, for the rest of the widgets user widget interactions would be a list of one single interaction element.

**API Definition:** [getWidgetInteractions](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getWidgetInteractions)

```javascript
import { getWidgetInteractions, WidgetKind } from '@livelike/javascript';

getWidgetInteractions({
  programId: "<your program Id>",
  widgetId: "xxxx",
  widgetKind: WidgetKind.TEXT_POLL
}).then(interactions => console.log(interactions))
```

## addWidgetListener

This API can be used to add a listener for widget result based events. This lets you react to options vote count updates in real time basis.

**API Definition:** [addWidgetListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addWidgetListener)

```javascript
import { addWidgetListener, WidgetKind } from '@livelike/javascript';

function widgetListener({ event, message }){
	// your custom logic
}

addWidgetListener({
 	widgetId: "<Your widget Id>",
  widgetKind: WidgetKind.IMAGE_POLL
}, widgetListener).then(() => console.log('listener added'));
```

## removeWidgetListener

This API is used to remove listeners attached using `addWidgetListener`.

**API Definition:** [removeWidgetListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=removeWidgetListener)

```javascript
import { removeWidgetListener, WidgetKind } from '@livelike/javascript';

function widgetListener({event, message}){
// your custom logic
}

removeWidgetListener({
 	widgetId: "<Your widget Id>",
 	widgetKind: WidgetKind.IMAGE_POLL
}, widgetListener).then(() => console.log('listener removed'));;
```

## getWidget

This API can be used to get any published widget details using its id and kind.\
**API Definition:** [getWidget](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getWidget)

```javascript
import { getWidget, WidgetKind } from '@livelike/javascript';

getWidget({
  widgetId: "******" ,
  widgetKind: WidgetKind.IMAGE_POLL
}).then(widgetPayload => console.log(widgetPayload));
```

## getUnclaimedWidgetInteractionsRewards

This API can be used to get interactions for widgets that have not yet had their rewards claimed.\
**API Definition:** [getUnclaimedWidgetInteractionsRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getUnclaimedWidgetInteractionsRewards)

```javascript
import { getUnclaimedWidgetInteractionsRewards } from '@livelike/javascript';

getUnclaimedWidgetInteractionsRewards({ 
  programId: "****"
}).then(widgetInteractions => console.log(widgetInteractions);
```

## getWidgets

This API can be used to fetch paginated List of Widgets filtered by widget status and kind.\
It takes a programId as a mandatory argument.\
Other optional parameters to filter the widget list are widget status, ordering, interactivity and an array of widget's kind.\
**API Definition:** [getWidgets](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getWidgets)

```javascript
import { getWidgets, WidgetKind } from '@livelike/javascript';

getWidgets({
  programId: "xxxx",
  status: "pending", //Valid status values are 'scheduled', 'pending', 'published'
  widgetKinds: [ WidgetKind.TEXT_POLL ],
  ordering: "recent", //Valid ordering values are 'recent'
  interactive: true,  //Valid interactive values are true, false
  // option widget attributes to get widgets based on certain attributes
  widgetAttributes: [ {key: "fruit", value: "apple"} ]
}).then(res => console.log(res));
```

## createWidgetImpression

This API lets you create an widget impression that could be used for analytics purposes, for eg: track the user reachability of a given widget as shown in producer suite application.

**API Definition:** [createWidgetImpression](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createWidgetImpression)

```javascript
import { createWidgetImpression, WidgetKind } from '@livelike/javascript';

createWidgetImpression({
	widgetId: "<Your widget Id>",
  widgetKind: WidgetKind.IMAGE_PREDICTION
}).then(res => console.log(res))
```

## createWidgetInteraction

This API lets you create a new widget interaction. Use this API when a user interacts with the widget UI for the first time.\
Before using this API, make sure you have already fetched widget details using either `getPostedWidgets`, `getWidgets` or `getWidget` API and also checked if there were no widget interaction present using `getWidgetsInteractions` or `getWidgetInteractions` API.\
In case of:

* Poll/Prediction/Cheer meter widget -> interaction item would be of type [IWidgetOptionItem](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetOptionItem). Use widget details `options` element to pass interaction item.
* Quiz widget -> interaction item would be of type [IWidgetChoiceItem](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetChoiceItem). Use widget details `choices` element  to pass interaction item. 
* Text ask widget -> interaction item would of type [ITextAskInteractionItem](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=ITextAskInteractionItem)
* Emoji slider widget -> interaction item would of type [ISliderInteractionItem](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=ISliderInteractionItem)
* Number Prediction widget -> interaction item would be of type  [INumberPredictionItem](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=INumberPredictionItem)

**API Definition:** [createWidgetInteraction](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createWidgetInteraction)

```javascript
import { createWidgetInteraction, WidgetKind } from '@livelike/javascript';

// Refer API definition for possible values of interaction item based on widget kind
const selectedPollOption = {
  // ...pollWidgetPayload.options[0]
}

createWidgetInteraction({
  widgetId: "<Your widget Id>",
  widgetKind: WidgetKind.IMAGE_PREDICTION
  interactionItem: selectedPollOption 
}).then(interaction => {
	console.log(interaction);
})
```

## updateWidgetInteraction

This API lets you update an existing user widget interaction which was already created by `createWidgetInteraction` API.\
Make sure to check whether a widget interaction is already created using `getWidgetsInteractions` or using `getWidgetInteractions` API. In case no widget interaction found, use `createWidgetInteraction` instead. 

**API Definition:** [updateWidgetInteraction](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=updateWidgetInteraction)

```javascript
import { updateWidgetInteraction, WidgetKind } from '@livelike/javascript';

// Refer API definition for possible values of interaction item based on widget kind
const selectedPollOption = {
  // ...pollWidgetPayload.options[0]
}

updateWidgetInteraction({
  widgetId: "<Your widget Id>",
  widgetKind: WidgetKind.IMAGE_PREDICTION
  interactionItem: selectedPollOptionItem
}).then(interaction => {
	console.log(interaction);
})
```

## claimPredictionWidgetRewards

This API lets you claim rewards in the case of prediction follow up widgets. For prediction based widgets like Text/Image Prediction or Image Number Prediction widget, rewards are needed to be claimed only after followup widget is published.\
This API works only with follow up widget details where follow up widget Id could be fetched using [real time widget details](javascript-widgets#real-time-published-widgets) or from producer suite.

**API Definition:** [claimPredictionWidgetRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=claimPredictionWidgetRewards)

```javascript
import { claimPredictionWidgetRewards, WidgetKind } from '@livelike/javascript';

claimPredictionWidgetRewards({
  widgetId: "<Your widget Id>",
  widgetKind: WidgetKind.IMAGE_PREDICTION
}).then(predictionClaim => {
	console.log(predictionClaim);
})
```

## getTargetedWidgetIdAndKind

This API gets targeted widget Id and widget kind for a given widget details. This API could be helpful for prediction follow up widget to get corresponding widgetId and widgetKind against which user interaction was performed. In case of non follow up widget details, this API would return same `widgetId` and `widgetKind`. You could pass either of the below argument props

1. `widget` (widget payload)
2. `widgetId` and `widgetKind`

**API Definition:** [getTargetedWidgetIdAndKind](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getTargetedWidgetIdAndKind)

```typescript javascript
import { getTargetedWidgetIdAndKind } from "@livelike/javascript"

getTargetedWidgetIdAndKind({
   widgetId: "xxxx",
   widgetKind: WidgetKind.TEXT_PREDICTION_FOLLOW_UP
 }).then(res => console.log(res))
 
// OR
getTargetedWidgetIdAndKind({
  widget: { // widgetPayload }
}).then(res => console.log(res))
```
