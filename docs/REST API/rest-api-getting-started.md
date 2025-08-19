---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Getting Started | REST API | LiveLike Developer Hub
  description: >-
    In order to use the REST API you must first create an application Client ID
    and obtain an Access Token. Learn more about REST APIs.
  robots: index
next:
  description: ''
---
In order to use the REST API you must first create an application Client ID and obtain an Access Token.

## Create an Application

An application can be created through LiveLike's [Producer Suite](https://cf-blast.livelikecdn.com/).  If you have not received an invitation please contact [LiveLike Support](mailto:support@livelike.com).

## Obtain an Access Token

You can provision an Access Token in the Application section of the [Producer Suite](https://cf-blast.livelikecdn.com/).  This is a standard OAuth 2.0 Bearer access token.  It can be used in HTTP requests by including it in the `Authorization` header like so:

```http
GET /api/v1/applications/{client-id}/ HTTP/1.1
Authorization: Bearer {access-token}
```