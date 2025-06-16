---
title: Get Widget Interactions
excerpt: ''
api:
  file: profiles.json
  operationId: get-widget-interactions
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
**Getting widget interaction url**

In order to make a widget interaction request you will need an access token.

The url can be retrieved using two of the following ways.

1. From the response of the widgets request in the program resource mentioned in the [Listing Widgets](ref:listing-widgets) section, under the property `widget_interactions_url_template`.  This url, when used in a `GET` request with a `profile_id` as the path param, will always return the first page of widget interactions, which includes interactions for all widgets.
2. Specific widgets can also be fetched by adding the query params of the widget kind as the key, with the matching widget id as the value. For example `?image_quiz_id=f1cb8aa8-941c-4278-92f5-127a70945ff6`
3. Interactions for widgets of a specific kind can be fetched using the `widget_kind` param. For example `?widget_kind=text-poll`.
4. Every widget interaction result will contain properties `next` and `previous`. These are optional urls that can be used in conjunction with your access token to retrieve more leaderboard entries.
