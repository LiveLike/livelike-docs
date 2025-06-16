---
title: useWidgetInteractedAnalytics
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
The `useWidgetInteractedAnalytics` hook is designed to track the Widget Interacted analytics event. It provides a function, `trackWidgetInteractedAction`, that you can use to track interactions with a specific widget.

##### Example usage

```typescript
const { trackWidgetInteractedAction } = useWidgetInteractedAnalytics({ widgetId: "<Widget ID>" });
```

## Hook Argument

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

## Hook Return Value

#### `trackWidgetInteractedAction`

| Type                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Function](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractedAnalytics) of type: ({ interactionItem:T }) => void |

interactionItem: The item representing the interaction with the widget.