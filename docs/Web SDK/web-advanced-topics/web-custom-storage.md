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
The Web SDK by default uses Local Storage as the storage mechanism for persistent data like <Glossary>Access Token</Glossary> and cached user data. If you prefer to use some other storage like cookies, you can do so by adding passing a `storageStrategy` property to `LiveLike.init`.

The `storageStrategy` property must be an object with a `get` and a `set` method.

## Example

```javascript
const localStorageStorageStrategy = {
  get: () => JSON.parse(localStorage.getItem('your-key')),
  set: (data) => localStorage.setItem('your-key', JSON.stringify(data))
}

LiveLike.init({
  clientId: "YOUR-CLIENT-ID",
  storageStrategy: localStorageStorageStrategy
})
```
