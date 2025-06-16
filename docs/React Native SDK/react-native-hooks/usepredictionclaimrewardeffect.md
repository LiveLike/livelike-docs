---
title: usePredictionClaimRewardEffect
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
`usePredictionClaimRewardEffect` hook claims the prediction reward whenever a prediction follow up based UI is rendered. Internally it calls [claimPredictionWidgetRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=claimPredictionWidgetRewards) JS API.

**Hook Type Definition**: [usePredictionClaimRewardEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=usePredictionClaimRewardEffect)

##### Example Usage:

```typescript react-native
import { usePredictionClaimRewardEffect } from "@livelike/react-native"
import { WidgetKind } from "@livelike/javascript"

const widgetId = "xxx-yyyy-zzz"
const widgetKind = WidgetKind.IMAGE_PREDICTION_FOLLOW_UP

usePredictionClaimRewardEffect({ widgetId, widgetKind });
```