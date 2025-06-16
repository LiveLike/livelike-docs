---
title: Widget API Methods
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget API Methods | Web SDK | LiveLike
  description: >-
    Web SDK contains various widget API methods that can be used to build custom
    widget modes. Learn more about widget API methods.
  robots: index
next:
  description: ''
---
Web SDK contains various widget API methods which can be used to build custom widget modes

## getPostedWidgets

This method can be used to get published widgets for the program.

This method takes a programId as argument

```javascript
LiveLike.getPostedWidgets({
  programId: "*****",
  // option widget attributes to get widgets based on certain attributes
  widgetAttributes: [ {key: "fruit", value: "apple"} ]
}).then(res => {
  console.log('res', res);
});
```

## getWidgetInteractions

This method can be used to get interactions for the user for a given set of widgets or for the interactionUrl returned form the timeline resource.

This method takes the interactionUrl, or a programId and an array of widget's kind and id.

Please note: For followup widgets, there are no interaction. They should be attached with the interaction on their corresponding prediction

```javascript
LiveLike.getWidgetInteractions({
  programId: "*****",
  widgets: [{ kind: "cheer-meter", id:"*****"}]
})
```

## addWidgetListener

This method can be used to execute any callback when a widget is received on the program channel.

```javascript
LiveLike.addWidgetListener(
  {programId: "*****"}, 
  (e) => console.log(e)
);
```

## removeWidgetListener

This method is used to remove listeners attached using addWidgetListener

```javascript
LiveLike.removeWidgetListener({programId: "*****"}, widgetHandler);
```

## getWidget

This method can be used to get any published widget using its id and kind.

```javascript
LiveLike.getWidget({ id: "******" , kind: "*****" }).then(widgetPayload =>
	console.log(widgetPayload);
);
```

## getUnclaimedRewards

This method can be used to get interactions for widgets that have not yet had their rewards claimed.

```javascript
const widgets = document.querySelector('livelike-widgets');
widgets.getUnclaimedRewards().then(widgetInteractions => 
	console.log(widgetInteractions);
);
```

## getWidgets

This method can be used to fetch paginated List of Widgets filtered by widget status and kind.

This method takes a programId as a mandatory argument.\
Other optional parameters to filter the widget list are widget status, ordering, interactivity and an array of widget's kind.

```javascript
getWidgets({
  programId: "xxxx",
  status: "pending", //Valid status values are 'scheduled', 'pending', 'published'
  widgetKinds: ["text-poll"],
  ordering: "recent", //Valid ordering values are 'recent'
  interactive: true  //Valid interactive values are true, false
  // option widget attributes to get widgets based on certain attributes
  widgetAttributes: [ {key: "fruit", value: "apple"} ]
}).then(res => console.log(res));
```
