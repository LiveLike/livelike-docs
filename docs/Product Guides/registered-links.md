---
title: Registered Links
excerpt: ''
deprecated: false
hidden: false
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
1. The **Name** is the label that will be shown when attaching links to other resources like badges and widgets
1. The **URL** is the target of the link
[block:api-header]
{
  "title": "Creating Registered Links"
}
[/block]
Registered links can be managed from inside the CMS.
1. To register a link, click on Registered Links menu item on the left hand side panel in the CMS
1. You will be presented with a list of already created Registered Links, which can be modified or deleted
1. To create a Registered Link, click on the **+ New Registered Link** button on the top right hand side
1. A prompt will be presented where you can fill in the new link's details and create a new registered link
[block:api-header]
{
  "title": "Utilizing Registered Links"
}
[/block]
Once a registered link is created it can be associated with other resources. Integrations are able to read registered link data attached to resources that have links associated with them.
[block:code]
{
  "codes": [
    {
      "code": "let sdk: EngagementSDK\n\n// Working with Registered Links in the Badge resource\nsdk.badges.getApplicationBadges(page: .first) { result in\n  switch result {\n  case .failure(let error):\n    print(\"Error: \\(error)\"            \n  case .success(let badges):\n    if let firstBadge = badges.items.first {\n      print(\"Registered Links amount: \\(firstBadge.registeredLinks.count)\")\n    }               \n  }\n}",
      "language": "swift"
    },
    {
      "code": "badgesClient.getApplicationBadges(\n\tLiveLikePagination.FIRST,\n  object :\n  \tLiveLikeCallback<LLPaginatedResult<Badge>>() {\n    \toverride fun onResponse(result: LLPaginatedResult<Badge>?, error: String?) {\n        result?.let{\n        \tprintln(\"Registered Links amount: ${result.result.size()}\")\n        }\n      }\n    })",
      "language": "kotlin"
    },
    {
      "code": "LiveLike.getApplicationBadges()\n.then(res =>\n  res.results.forEach(badge => console.log('registered link for badge', badge.registered_links))\n);",
      "language": "javascript"
    }
  ]
}
[/block]