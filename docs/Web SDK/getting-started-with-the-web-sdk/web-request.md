---
title: Web API Requests
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
In case you feel the need to use our backend REST API due to some extreme edge cases that our SDK API doesn't support, you can use `request` API that is also internally used by our SDK to make any backend request.

## Request interface

`request` API lets you easily make a backend request without needing to manually create needed endpoints with set of query parameters, add authorisation token in a given format, etc.

```javascript Web
LiveLike.request({
  path: '/user-quest-rewards/',
  // queryParams could be list of string or just string
  // list of string is useful to include query params with same key
  // for eg: <url>?fruit=apple&fruit=orange
  queryParams: {
    "user_quest_id": [ "user-quest-id-1", "user-quest-id-2", "user-quest-id-3" ],
    "reward_status": LiveLike.QuestRewardStatus.CLAIMED
  },
  method: LiveLike.HTTP_METHOD.GET,
  headers: {
    // any custom headers to be included
  }
}).then(res => console.log(res))
```

## Authorization

In case you need to pass your own authorisation token, you can use `createUserProfileAuth`or `createPersonalApiAuth` API that takes a token string as argument and returns authorisation value

### Profile access token authorization

```typescript Web
const accessToken = LiveLike.userProfile.access_token;
LiveLike.request({
    auth: LiveLike.createUserProfileAuth(accessToken),
  	// rest of the request args 
}).then(res => console.log(res))
```

### Personal API token authorization

Be extra careful when defining and accessing personal API token, for eg: do not commit personal API token in code base and inject it using environment variables

```typescript Web
const personApiToken = ENV.PERSONAL_API_TOKEN;
LiveLike.request({
    auth: LiveLike.createPersonalApiAuth(personApiToken),
  	// rest of the request args 
}).then(res => console.log(res))
```
