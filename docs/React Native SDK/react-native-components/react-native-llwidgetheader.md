---
title: LLWidgetHeader
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
> 🚧 Pre-requisite
> 
> Make sure you [initialise React Native SDK](react-native-getting-started#initialise-react-native-sdk).

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7baefa3-Group_68_1.svg",
        null,
        "Widget header Anatomy"
      ],
      "align": "center",
      "sizing": "600px",
      "caption": "Widget Header Anatomy"
    }
  ]
}
[/block]

`LLWidgetHeader` is a fundamental atomic component that is used by various widget components. This component is rendered as a top component as part of [widget anatomy](react-native-widget-anatomy).

```typescript react native
import { LLWidgetHeader } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetHeader() {
  const interactiveTimeoutHandler = () => {
    // your custom logic
  }
  return (
    <LLWidgetHeader
      title="Who scored more goals in last FIFA?"
      // number of milliseconds since EPOC (Date.now() or new Date().getTime())
      interactiveTimeout="1684926773919"
      dismissable={true}
      onInteractiveTimeout={interactiveTimeoutHandler}
    />
  );
}
```

## Hooks used by `LLWidgetHeader`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)

## Component Hierarchy

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a430993-Widget_Doc-Component_hierarchy.drawio.svg",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

## LLWidgetHeader Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `title`

| Type   | Default    |
| :----- | :--------- |
| String | No Default |

`title` refers to the `title` or `question` in widget payload.  

#### `dismissable`

| Type    | Default |
| :------ | :------ |
| Boolean | false   |

If dismissable, show close icon which when pressed removes the widget from the UI.

#### `onDismiss`

| Type     | Default    |
| :------- | :--------- |
| Function | No Default |

Function that gets invoked whenever user dismisses the widget by clicking on dismiss Icon.

#### `interactiveTimeout`

| Type   | Default    |
| :----- | :--------- |
| Number | No default |

Interactive timeout in [epoch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date). Once the timeout gets elapsed, widget transition into `Timed Out` phase where it is in disabled state.
When setting `interactiveTimeout` as `null`, this overrides widget interactive timeout (that is set from producer suite) and widget becomes always interactive.

#### `onInteractiveTimeout`

| Type     | Default    |
| :------- | :--------- |
| Function | No Default |

Function that gets invoked whenever interactive timer gets elapsed. When `interactiveTimeout` is set to `null`, onInteractiveTimeout function would never be called.

#### `styles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetHeaderStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetHeaderStyles` |

#### `WidgetInteractiveTimerComponent`

| Type                                                                                                                                        | Default                                                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetInteractiveTimer](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetInteractiveTimer) | [LLWidgetInteractiveTimer](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetInteractiveTimer) |

Horizontal timer component rendered whenever based on `interactiveTimeout` value. The timer components updates the progress on every `500ms`. To customise rendered timer component or customise `updateInterval`, pass your own custom timer component or extend `LLWidgetInteractiveTimer` component by setting required props.

##### Example usage:

```typescript React Native
import { LLWidgetHeader, LLWidgetInteractiveTimerProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

// Widget header with custom timer component
function MyTimerComponent(props: LLWidgetInteractiveTimerProps){
  // your own custom timer implementation
}

function MyWidgetHeader() {
  return (
    <LLWidgetHeader
      title="Who scored more goals in last FIFA?"
      // number of milliseconds since EPOC (Date.now() or new Date().getTime())
      interactiveTimeout="1684926773919"
      dismissable={true}
      WidgetInteractiveTimerComponent={MyTimerComponent}
    />
  );
}

// Widget header with customised stock Timer component
function CustomTimerComponent(props: LLWidgetInteractiveTimerProps){
  // as an example, we are customising stock timer component behaviour by setting updateInterval prop 
  return <LLWidgetInteractiveTimer {...props} updateInterval={1000}/>
}

export function WidgetHeader() {
  return (
    <LLWidgetHeader
      title="Who scored more goals in last FIFA?"
      // number of milliseconds since EPOC (Date.now() or new Date().getTime())
      interactiveTimeout="1684926773919"
      dismissable={true}
      WidgetInteractiveTimerComponent={CustomTimerComponent}
    />
  );
}
```

#### `WidgetInteractiveTimerComponentStyles`

| Type                                                                                                                                                     | Default                                                                                                  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetInteractiveTimerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetInteractiveTimerStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetInteractiveTimerStyles` |

`LLWidgetInteractiveTimerStyles` prop which could be used to modify styles of default rendered `LLWidgetInteractiveTimer` component.

#### `DismissIconComponent`

| Type                                                                                                                                          | Default                                                                                                                   |
| :-------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetHeaderDismissIcon](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetHeaderDismissIcon) | [LLWidgetHeaderDismissIcon](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetsLoadMoreButton) |

Dismiss icon component which when pressed removes the widget from the UI. In case needed, pass your own custom icon component. 

##### Example usage:

```typescript React Native
import { LLWidgetHeader, LLWidgetHeaderDismissIconProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

// Widget header with custom timer component
function MyDismissIconComponent(props: LLWidgetHeaderDismissIconProps){
  // your own custom dismiss icon component
}

function MyWidgetHeader() {
  return (
    <LLWidgetHeader
      title="Who scored more goals in last FIFA?"
      dismissable={true}
      DismissIconComponent={MyDismissIconComponent}
    />
  );
}
```

#### `DismissIconComponentStyles`

| Type                                                                                                                                             | Default                                                                                              |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------- |
| StyleSheet of type [DismissIconComponentStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=DismissIconComponentStyles) | No Default, if present styles props would be applied on top of internal `DismissIconComponentStyles` |

`DismissIconComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetHeaderDismissIcon` component.