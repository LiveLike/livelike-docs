---
title: useWidgetSubmitAction
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
The `useWidgetSubmitAction` hook is designed to enable the tracking of Widget Submitted analytics events and manage the widget interaction submit action. It internally calls `createWidgetInteractionAction` to ensure analytics tracking is executed upon successful resolution.

##### Example usage

It returns an object with the onInteractionSubmit function that you can use to handle the submission of widget interactions.

```typescript
const { onInteractionSubmit } = useWidgetSubmitAction({ widgetId: "<Widget ID>" });
```

## Hook Argument

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

## Hook Return Value

#### `onInteractionSubmit`

| Type                                                                                                                                                                                                                                                                                                                                                                                                               |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Function](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetSubmitAction) of type: ({ interactionItem:[WidgetCreateInteractionActionArg](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=WidgetCreateInteractionActionArg) }) => Promise\<void \| [IWidgetInteraction](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetInteraction)> |

interactionItem: The item representing the interaction with the widget.