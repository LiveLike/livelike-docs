---
title: LLCoreWidget
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
`LLCoreWidget` is a container component used by various widget component where it is usually the first component rendered in the component hierarchy of a widget. This component is responsible for:

* Loading widget details based on `widgetId` and `widgetKind` using [useLoadWidgetEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useLoadWidgetEffect) hook.
* Add dismiss functionality using [useWidgetDismiss]().
* Render `LoadingComponent` when widget details are been loaded.
* Render `ErrorComponent` when there was an error loading widget details.
* Render widget UI using `children` prop.

## Hooks used by `LLCoreWidget`

* [useLoadWidgetEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useLoadWidgetTimelineEffect)
* [useWidgetDismiss](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetDismiss)
* [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)

## LLCoreWidget Props

> 📘 Customisation
>
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `programId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

This is the Id of the program in which a given set of  widgets are published from producer suite.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `widgetKind`

| Type                                                                                                    | Default    |
| :------------------------------------------------------------------------------------------------------ | :--------- |
| [WidgetKind](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=WidgetKind) (**Required**) | No Default |

#### `styles`

| Type                                                                                                                             | Default                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| Stylesheet of type [LLCoreWidgetStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidgetStyles) | No Default, if present styles props would be applied on top of internal `LLCoreWidgetStyles`. |

#### `LoadingComponent`

| Type            | Default                                                                                          |
| :-------------- | :----------------------------------------------------------------------------------------------- |
| React Component | [ActivityIndicator](https://reactnative.dev/docs/activityindicator) as default Loading component |

Component to render when widget details are being loaded.

##### Example usage:

```typescript React Native
import React from 'react';
import { LLCoreWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';
import { View, Text } from 'react-native';

const CustomLoadingComponent = () => {
  return (
    <View>
      <Text> Loading Widget... </Text>
    </View>
  );
};

export function MyWidget() {
  return (
    <LLCoreWidget
      programId="xxxxx"
      widgetId="yyyy"
      widgetKind={WidgetKind.TEXT_POLL}
      LoadingComponent={CustomLoadingComponent}
    >
      {({ widget, onDismiss }) => {
        // render widget UI
      }}
    </LLWidget>
  );
}
```

#### `ErrorComponent`

| Type            | Default                                                             |
| :-------------- | :------------------------------------------------------------------ |
| React Component | View and Text component showing `Unable to load widgets` error text |

Component to render whenever there's an error in loading widget.

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';
import { View, Text } from 'react-native';

const CustomErrorComponent = () => {
  return (
		<View>
    	<Text style={{ color: 'red' }}> Ohh snap! widgets not loaded </Text>
    </View>
  );
};

export function MyWidget() {
  return (
    <LLWidget
      programId="xxxxx"
      widgetId="yyyy"
      widgetKind={WidgetKind.TEXT_POLL}
      ErrorComponent={CustomErrorComponent}
    >
      {({ widget, onDismiss }) => {
        // render widget UI
      }}
    </LLWidget>
  );
}
```

#### `onDismiss`

| Type     | Default    |
| :------- | :--------- |
| Function | No Default |

Function that gets invoked whenever user dismisses the widget by clicking on dismiss Icon that is rendered as part of widget header.

#### children

| Type                                                                                                                                              | Default    |
| :------------------------------------------------------------------------------------------------------------------------------------------------ | :--------- |
| (props: [LLCoreWidgetChildrenProps](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidgetChildrenProps)) => ReactNode | No Default |

`children` prop for LLCoreWidget that is called with prop [LLCoreWidgetChildrenProps](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidgetChildrenProps)

##### Example usage:

```typescript React Native
import React from 'react';
import { LLCoreWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';


export function MyWidget() {
  return (
    <LLCoreWidget
      programId="xxxxx"
      widgetId="yyyy"
      widgetKind={WidgetKind.TEXT_POLL}
      ErrorComponent={CustomErrorComponent}
    >
      {({ widget, onDismiss }) => { // core widget calling children prop function with widget, onDismiss 
        // render widget UI
      }}
    </LLWidget>
  );
}
```
