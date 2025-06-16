---
title: Reward Items
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
      slug: reward-actions-copy
      title: Reward Actions
---
## Retrieve all Reward Items linked to an Application

All reward items linked to an [application](https://docs.livelike.com/docs/rest-api-getting-started#create-an-application) can be retrieved using the `getApplicationRewardItems` function.

**API Definition**:  [getApplicationRewardItems](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getApplicationRewardItems)

```javascript javascript
import { getApplicationRewardItems } from "@livelike/javascript"

getApplicationRewardItems().then(res => {
  console.log('res', res);
});
```



## Reward Item Attributes

Reward Item Attributes provide integrators with organisational and filtering tools.  
These attributes are key, value pairs of data defined in the LikeLive CMS portal.

In addition when retrieving reward items, attributes can be used to filter reward item result sets.

```javascript
import { getApplicationRewardItems } from "@livelike/javascript"

const attributes = [{key: "color", value: "blue"}]
  
getApplicationRewardItems({ attributes }).then(res => {
  res.results.forEach((rewardItem) => {
  	console.log(rewardItem.attributes)
  })
});
```



## Reward Item Images

Reward Item Images enable integrators to visually enhance and customize their user experience

```javascript
import { getApplicationRewardItems } from "@livelike/javascript"

getApplicationRewardItems()
.then(res =>
	res.results.forEach(rewardItem => console.log(rewardItem.images))
)
```



## Retrieving Reward Item Balances for the current user

As an integrator you have the ability to check the reward item balance the current user has. This can be done by utilizing the `getRewardItemBalances` function where you pass IDs of reward items you are interested in.

**API Definition**:  [getRewardItemBalances](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getRewardItemBalances)

```javascript javascript
import { getRewardItemBalances } from "@livelike/javascript"

getRewardItemBalances({ 
  rewardItemIds: ["xxx", "xxx"] 
}).then(res => console.log(res))
```



## Transferring Reward Item Amount to another User

To build out experiences such as gifting, tipping or just transferring Reward Item amounts to another user, you can use the `transferRewardItemAmount` function.

 **API Definition**:  [transferRewardItemAmount](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=transferRewardItemAmount)

```javascript javascript
import { transferRewardItemAmount } from "@livelike/javascript"

transferRewardItemAmount({ 
  rewardItemId: "xxx",
  recipientProfileId: "xxx",
  amount: 10
}).then(res => console.log(res))
```



## Retrieving Reward Item Transfers for the current user

As an integrator you can retrieve the paginated list of reward item transfers the current user has done. This can be done by utilizing the `getRewardItemTransfers` function.

 **API Definition**:  [getRewardItemTransfers](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getRewardItemTransfers) 

```javascript javascript
import { getRewardItemTransfers } from "@livelike/javascript"

getRewardItemTransfers().then(res => {
  console.log('res', res);
});
```



## Filtering Reward Item Transfers for the current user

As an integrator, you can filter reward item transfers the current user has done. Filtering can be done based on [`RewardItemTransferType`](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=RewardItemTransferType) which allows filtering the sent or received transfers.  This can be done by utilizing the `getRewardItemTransfers` function as mentioned below

 **API Definition**:  [getRewardItemTransfers](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getRewardItemTransfers) 

```javascript
import { getRewardItemTransfers, RewardItemTransferType } from "@livelike/javascript"

getRewardItemTransfers({
   transferType: RewardItemTransferType.RECEIVED
}).then(res => console.log(res))
```



## Notifying when Reward Item Transfer is received

As an integrator, you can inform users when they receive a new Reward Item Transfer.  
Use `addRewardEventListener` API for adding a listener function and `removeRewardEventListener` API for removing an added listener function.  
Using the RewardItemTransfer object, you can create a notification with appropriate information to the user.

**API Definition**: [addRewardEventListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addRewardEventListener), [removeRewardEventListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=removeRewardEventListener)  

```javascript
import { 
  addRewardEventListener,
  removeRewardEventListener,
  RewardEvent
} from "@livelike/javascript"

const onRewardListener = ({event, message: rewardItemTransfer}) => console.log(transferDetails)

// this adds a listener function that gets called whenever a reward 
// item transfer event occurs for the current user profile 
addRewardEventListener(
  RewardEvent.REWARD_ITEM_TRANSFER_RECEIVED, 
  onRewardListener
)

removeRewardEventListener(
  RewardEvent.REWARD_ITEM_TRANSFER_RECEIVED, 
  onRewardListener
)
```



## Retrieving earned rewards filtered by widgets

An integrator can retrieve rewards earned (filtered by widget types and widget IDs) using SDK interface method `getRewardTransactions`.

`getRewardTransactions` takes arguments where the widget types and widget IDs can be specified. 

**API Definition**: [getRewardTransactions](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getRewardTransactions)

```javascript javascript
import { getRewardTransactions, WidgetKind } from "@livelike/javascript"

// for getting rewards earned by user for a given widgetIds
getRewardTransactions({
  widgetIds: ["xx", "yy"],
}).then(res => console.log(res));

// for getting rewards by a given user profile
getRewardTransactions({
  widgetKinds: [ WidgetKind.TEXT_POLL, WidgetKind.TEXT_PREDICTION ],
}).then(res => console.log(res));

// all filetr parameters for getting rewards earned
getRewardTransactions({
  // any combination of these argument properties would work
  widgetIds: ["xx", "yy"],
  widgetKinds: ["text-poll", "text-prediction"],
  profileIds: ["xx-yy", "yy-zz"],
  rewardItemIds: ["123", "456"],
  rewardActionKeys: ["quiz-correct", "prediction-correct"],
  createdSince: '2022-06-01',
  createdUntil: '2022-07-31',
}).then(res => console.log(res));
```



## Retrieving potential widget rewards

Detailed information on potential earn-able rewards are attached to widget details.  
Use [getWidgets](javascript-widgets#getWidgets) or [getWidget](javascript-widgets#getWidget) API to get widget details.

```javascript javascript
import { getWidget, WidgetKind } from "@livelike/javascript"

getWidget({
  widgetId: "xxxx",
  widgetKind: WidgetKind.TEXT_POLL,
}).then((widgetDetails) => {
  console.log('widget Id', widgetDetails.id, widgetDetails.earnable_rewards);
  widgetDetails.options.forEach((option) => {
    console.log('option id', option.id, option.earnable_rewards)
  });
});
```