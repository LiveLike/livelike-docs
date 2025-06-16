---
title: Custom Storage
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Storage | Web SDK | LiveLike Developer Hub
  description: >-
    The Web SDK uses local storage as the storage mechanism for data like cached
    user data and more. Learn more about custom storage.
  robots: index
next:
  description: ''
---
The Web SDK by default uses Local Storage as the storage mechanism for persistent data like <<glossary:Access Token>> and cached user data. If you prefer to use some other storage like cookies, you can do so by adding passing a `storageStrategy` property to `LiveLike.init`.

The `storageStrategy` property must be an object with a `get` and a `set` method.
[block:api-header]
{
  "title": "Example"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "const localStorageStorageStrategy = {\n  get: () => JSON.parse(localStorage.getItem('your-key')),\n  set: (data) => localStorage.setItem('your-key', JSON.stringify(data))\n}\n\nLiveLike.init({\n  clientId: \"YOUR-CLIENT-ID\",\n  storageStrategy: localStorageStorageStrategy\n})",
      "language": "javascript"
    }
  ]
}
[/block]