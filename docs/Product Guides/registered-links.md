---
title: Registered Links
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: Registered Links | LiveLike Developer Hub
  description: >-
    A registered link is a link that exists within the LiveLike ecosystem and
    can be managed by producers through the CMS. Learn more.
  robots: index
next:
  description: ''
---
Registered Links allow marketing and editorial teams to more effectively collaborate within LiveLike. Once a link has been registered it can be attached to various resources, like [badges](doc:badges). Some use cases include:

* Sending traffic to affiliate or referral links
* Managing click-through and impression URLs for sponsors
* Implementing custom calls to action

A registered link consists of the following properties:

1. The **ID** is the unique identifier of the link
2. The **Name** is the label that will be shown when attaching links to other resources like badges and widgets
3. The **URL** is the target of the link

## Creating Registered Links

Registered links can be managed from inside the CMS.

1. To register a link, click on Registered Links menu item on the left hand side panel in the CMS
2. You will be presented with a list of already created Registered Links, which can be modified or deleted
3. To create a Registered Link, click on the **+ New Registered Link** button on the top right hand side
4. A prompt will be presented where you can fill in the new link's details and create a new registered link

## Utilizing Registered Links

Once a registered link is created it can be associated with other resources. Integrations are able to read registered link data attached to resources that have links associated with them.

```swift
let sdk: EngagementSDK

// Working with Registered Links in the Badge resource
sdk.badges.getApplicationBadges(page: .first) { result in
  switch result {
  case .failure(let error):
    print("Error: \(error)"            
  case .success(let badges):
    if let firstBadge = badges.items.first {
      print("Registered Links amount: \(firstBadge.registeredLinks.count)")
    }               
  }
}
```
```kotlin
badgesClient.getApplicationBadges(
	LiveLikePagination.FIRST,
  object :
  	LiveLikeCallback<LLPaginatedResult<Badge>>() {
    	override fun onResponse(result: LLPaginatedResult<Badge>?, error: String?) {
        result?.let{
        	println("Registered Links amount: ${result.result.size()}")
        }
      }
    })
```
```javascript
LiveLike.getApplicationBadges()
.then(res =>
  res.results.forEach(badge => console.log('registered link for badge', badge.registered_links))
);
```