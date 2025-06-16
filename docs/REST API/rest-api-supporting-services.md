---
title: Supporting Services
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Some features are developed with other partners and services. When using SDKs, those partner integrations are pre-configured and work out of the box. When using the REST API though, their configuration details are provided, but utilizing them is the developer's responsibility.
[block:api-header]
{
  "title": "Chat"
}
[/block]
The default chat driver is powered by [PubNub](https://pubnub.com/). When using an SDK, the initialization process is handled on your behalf and uses the PubNub SDK internally. For integrations that are not using an SDK, Application resources include a PubNub *subscribe key* that should be used to initialize the PubNub SDK. Profile access tokens can be treated as PubNub *auth keys*.
[block:api-header]
{
  "title": "Live Updates"
}
[/block]
Live updates are provided by [PubNub](https://www.pubnub.com/). These subscriptions allow clients to be notified of events quickly and without having to poll on the API. When using an SDK, the initialization process is handled on your behalf and uses the PubNub SDK internally. For integrations that are not using an SDK, Application resources include a PubNub *subscribe key* that should be used to initialize the PubNub SDK. 

A client can subscribe to resources like programs and widgets by subscribing to the resource’s *channel*. The channel name is usually found in the `channel_name` field of the resource. Live updates will be delivered as *messages*, a.k.a. *events*.