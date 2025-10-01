---
title: useDebounce
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The `useDebounce` hook is designed to delay the execution of a provided function until a specified time period has elapsed. This is particularly useful for scenarios where you want to wait for a user to stop typing or interacting with an input field before triggering a time-consuming operation, such as fetching data from an API.

##### Example usage

The useDebounce hook returns a debounced function. You can use this debounced function in your components to delay the execution of the provided function.

```typescript
const debouncedFunction = useDebounce({
    callback: ()=>{ console.log("Executed the debounced function after 1000 milliseconds") },
    timer: 1000,
});
```

## Hook Argument

[useDebounceArgs](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useDebounceArgs)

#### `callback`

| Type                    | Default    |
| :---------------------- | :--------- |
| Function (**Required**) | No Default |

#### `timer`

| Type                  | Default    |
| :-------------------- | :--------- |
| Number (**Required**) | No Default |

## Hook Return Value

The hook returns a debounced function that you can use to delay the execution of the provided function.
