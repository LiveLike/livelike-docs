---
title: useWidgetExpiryEffect
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
`useWidgetExpiryEffect` hook runs a timer to update widget UI phase to `EXPIRED` once the expiry time has passed. Expiry time is set when creating widget from producer suite.

**Hook Type Definition**: [useWidgetExpiryEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)

##### Example Usage:

```typescript
import { useWidgetExpiryEffect } from "@livelike/react-native"

const widgetId = "xxx-yyyy-zzz"

useWidgetExpiryEffect({ widgetId });
```
