---
title: Package structure
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
      slug: react-native-customisation
      title: Customisation
---
React Native package has a peer dependencies on our `@livelike/javascript` package which host all JS based LiveLike service API's.

The package in its core exports and contains:

#### 1. UI Components:

* Container components which adds UI state + basic logic to render presentational components.
* Presentational/Dummy atomic components which could be reused.  

#### 2. React Hooks:

Our stock UI uses these react hooks to drive the UI state.\
This hooks contains state data used for rendering presentational components and also contains handler functions to trigger UI interaction.\
Refer react hooks documentation.

Beside the exported component and hooks, you could use JS API from `@livelike/javascript` to implement your custom UI or custom logic as per your business needs.\
Refer Javascript package documentation for more details on the JS API's.

For customisation, browse to our next section which would give you an overview on different level of customisation and how could you compose these components.
