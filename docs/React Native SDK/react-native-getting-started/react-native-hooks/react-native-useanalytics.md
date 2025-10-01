---
title: useAnalytics
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
The `useAnalytics` hook is designed to facilitate custom analytics integration within your application. It allows you to set a custom analytics provider and provides a `trackEvent` function that can be used to track crucial events in your custom components.

Hook Type definition: [useAnalytics](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useAnalytics)

##### Example usage

```typescript
const { getAnalyticsProvider, setAnalyticsProvider, trackEvent  } = useAnalytics();
```

## Hook Return Value

#### `getAnalyticsProvider`

A function to get custom analytics provider.

| Type                                                                                                                                  |
| :------------------------------------------------------------------------------------------------------------------------------------ |
| Function of type: () => [IAnalyticsProvider](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IAnalyticsProvider) |

#### `setAnalyticsProvider`

A function to set a custom analytics provider dynamically

| Type                                                                                                                                                |
| :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| Function of type: (provider: [IAnalyticsProvider](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IAnalyticsProvider)) => void |

#### `trackEvent`

A function that allows you to track custom events.

| Type                                                         |
| :----------------------------------------------------------- |
| Function of type: (event: string, trackObj: unknown) => void |
