---
title: Reward Actions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Reward Actions | JavaScript SDK | LiveLike
  description: >-
    Reward Actions are used to trigger the reward engine for given built-in or
    custom actions on a JavaScript SDK platform. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-leaderboards
      title: Leaderboards
---
Reward Action are used to trigger the reward engine for the given action. There are already built in reward actions already defined in producer suite where producer/integrators could also create their own custom reward actions.

Some example of custom reward actions could be:

1. Opening an app once a day
2. Completing an on-boarding process
3. Reading an article
4. Watching a video

## Creating a Custom Reward Action

1. In producer suite, browse to the "Rewards" section from the left navigation panel.
2. Click on Actions tab which will show you list of all available reward actions.
3. Click on "New Reward Action" button, fill in the required details and click "Create".

## List of all Reward Actions

Get the list of all reward actions. Each list item is a reward action object that contains a "key" property which could be used to fetch invoked reward actions for a given program id. 

**API Definition**:  [getRewardActions](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getRewardActions)

```javascript
import { getRewardActions } from "@livelike/javascript"

getRewardActions().then(res => {
  console.log('res', res);
});
```



## List of all invoked Reward actions

Get the list of all the invoked reward actions for a given program. 

**API Definition**:  [getInvokedRewardActions](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getInvokedRewardActions)

```javascript
import { getInvokedRewardActions } from "@livelike/javascript"

getInvokedRewardActions({
  programId: "xxx-yyy-zzz"
}).then(res => {
  console.log('res', res);
});
```



further filters can be supplied to narrow down your results.

filters include:

- reward action keys
- profile ids to limit to specific users
- attributes to filter on integration supplied data

```javascript
import { getInvokedRewardActions } from "@livelike/javascript"

getInvokedRewardActions({
  rewardActionKeys: ["xx-yy-zz"],
  profileIds: ["xxx-yyy", "www-zzz"],
  attributes: [{ key: "color", value: "red" }]
}).then(res => {
  console.log('res', res);
});
```