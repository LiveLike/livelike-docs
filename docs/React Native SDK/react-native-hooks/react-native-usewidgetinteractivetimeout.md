---
title: useWidgetInteractiveTimeout
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
The purpose of `useWidgetInteractiveTimeout` hook is to derive resulted `interactiveTimeout` based on the passed interactiveTimeout value that in turns drives widget UI phases. For example, once the widget timeouts, widget UI phase would transition from `INTERACTIVE` to `TIMED_OUT` which would turn the widget into a non interact-able widget. Resulted `interactiveTimeout` value is used by `LLWidgetHeader`.  
You could pass `interactiveTimeout` as `null` in case you want widget to be always interact-able. 

**Hook Type Definition**: [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)

##### Example Usage:

```typescript
import { useWidgetInteractiveTimeout } from "@livelike/react-native"

// passing a custom interactive timeout of 3 second
const myInteractiveTimeout = 3000
// handler fn called when widget timeouts
const onInteractiveTimeoutHandler = () => {
 // your custom logic
}

const { 
  interactiveTimeout,
  onInteractiveTimeout 
} = useWidgetInteractiveTimeout({
  widgetId,
  interactiveTimeout: myInteractiveTimeout,
  onInteractiveTimeout: onInteractiveTimeoutHandler,
});
```