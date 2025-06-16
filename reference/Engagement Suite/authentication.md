---
title: Authentication
excerpt: Authenticating with LiveLike credentials
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
All requests are authenticated with OAuth 2 Bearer authentication provided through the Authorization HTTP header. The value of the header must include an <<glossary:Access Token>>.

```text Authorization Header
Authorization: Bearer your-access-token
```

Access Tokens can be obtained by creating a [Profile](doc:user-profiles) through the API or SDKs, or from inside the [Producer Suite](doc:retrieving-important-keys).

## Profile Access Token

Access Tokens that are obtained by creating a profile are also called Profile Access Tokens, and are scoped to that profile. They are used to do things like interact with widgets and participate in chat.

> 📘 Use Profile Access Tokens to represent end-users in your app.
> 
> Use Profile Access Tokens when interacting with widgets and chat on behalf of a particular end user in your application.

## Admin Access Token

Admin Access Tokens are scoped to an application and have broader scopes and permissions than Profile Access Token. They are are scoped to an Application and associated with a Producer. These tokens can be used to create and publish new widgets and perform moderation duties. 

> 📘 Use Admin Access Tokens for server-to-server automations.
> 
> Use Admin Access Tokens in management and integration scenarios like automatically creating programs and publishing widgets. Don't use API Access Tokens to represent end-users in your app.

> ❗️ Keep Admin Access Tokens secret!
> 
> Be cautious with Admin Access Tokens, they are quite permissive and are generally not necessary for client-side integrations.

Admin Access Tokens are also sometimes referred to as API Access Tokens and Producer Access Tokens.

## Personal API Token

Personal API Tokens allow you to perform site-wide and organization-wide administrative tasks such as creating and managing applications.  A Personal API Token can be obtained from the My Account page in the LiveLike Producer CMS.

```text
Authorization: Token your-personal-api-token
```

> ❗️ Keep Personal API Tokens secret!
> 
> Be cautious with Personal API Tokens, they are quite permissive and are generally not necessary for client-side integrations.