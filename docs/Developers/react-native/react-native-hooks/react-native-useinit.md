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

```typescript
const { profile, loaded } = useInit({
  clientId: '<Client ID>',
});
```

## Hook argument

> 📘 JS API `init` args reference
>
> Both, JS API `init` and `useInit` hook use the same argument details.\
> Browse our [`init` args description](javascript-getting-started) in case you need to understand `useInit` args.

## Hook Return Value

#### `profile`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [IUserProfile](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface-IUserProfile)
      </td>

      <td>
        null
      </td>
    </tr>
  </tbody>
</Table>

#### `loaded`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        boolean
      </td>

      <td>
        false
      </td>
    </tr>
  </tbody>
</Table>
