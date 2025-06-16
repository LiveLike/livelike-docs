---
title: useInit
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
      slug: usechatroom
      title: useChatRoom
---
The purpose of `useInit` hook is to  initialise the SDK as an alternative to `init` JS API. Internally it uses `init` JS API, creates a new user profile if no user profile token is passed or reuses existing user profile in case a user token is passed.

##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "const { profile, loaded } = useInit({\n  clientId: '<Client ID>',\n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hook argument"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "JS API `init` args reference",
  "body": "Both, JS API `init` and `useInit` hook use the same argument details.\nBrowse our [`init` args description](javascript-getting-started) in case you need to understand `useInit` args."
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `profile`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[IUserProfile](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface-IUserProfile)",
    "0-1": "null"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `loaded`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "boolean",
    "0-1": "false"
  },
  "cols": 2,
  "rows": 1
}
[/block]