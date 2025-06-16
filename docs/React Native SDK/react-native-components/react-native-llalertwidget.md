---
title: LLAlertWidget
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

`LLAlertWidget` is a info based read only widget UI component.

```javascript react native
import { LLAlertWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetContainer() {
  return (
    <LLAlertWidget
      programId="xxxxx"
      widgetId="yyyyy"
    />
  );
}
```

### Hooks used by `LLAlertWidget`

- [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)

### LLAlertWidget Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `programId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

This is the Id of the program in which a given widget is published 

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |


#### `onDismiss`

| Type     | Default    |
| :------- | :--------- |
| Function | No Default |

Function that gets invoked whenever user dismisses the widget by clicking on dismiss Icon.  
Pass `onDismiss` prop (with no op function) to make widget `dismissible`.

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

Function that gets invoked whenever interactive timer gets elapsed. When `interactiveTimeout` is set to `null`, `onInteractiveTimeout` function would never be called.

#### `WidgetComponent`

| Type                                                                                                                | Default                                                                                           |
| :------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------ |
| Component of type [LLCoreWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidget) | [LLCoreWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidget) |

This is the core widget component that is responsible for loading widget details and rendering other part of widget UI (passed as children).  
Refer [LLCoreWidget](react-native-llcorewidget) docs for more details. 

#### `WidgetComponentStyles`

| Type                                                                                                                             | Default                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLCoreWidgetStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCoreWidgetStyles) | No Default, if present styles props would be applied on top of internal `LLCoreWidgetStyles` |

`WidgetComponentStyles` prop that could be used to modify styles of default rendered `LLCoreWidget` component.

#### `HeaderComponent`

| Type                                                                                                                    | Default                                                                                               |
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetHeader) | [LLWidgetHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetHeader) |

Refer [LLWidgetHeader](react-native-llwidgetheader) docs for more details.

##### Example usage:

```typescript React Native
import { LLAlertWidget, LLWidgetHeaderProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLAlertWidget
      programId="xxxxx"
      widgetId="yyyyy"
      HeaderComponent={MyHeaderComponent}
    />
  );
}
```

#### `HeaderComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetHeaderStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetHeaderStyles` |

`HeaderComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetHeader` component.

#### `SponsorComponent`

| Type                                                                                                                    | Default                                                                                               |
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetSponsor](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsor) | [LLWidgetSponsor](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsor) |

Component responsible for rendering widget sponsor (based on sponsor selected in producer suite for a given widget).

##### Example usage:

```typescript React Native
import { LLAlertWidget, LLWidgetSponsorProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MySponsorComponent(props: LLWidgetSponsorProps){
  // your custom widget sponsor component
}

function MyWidget() {
  return (
    <LLAlertWidget
      programId="xxxxx"
      widgetId="yyyyy"
      SponsorComponent={MySponsorComponent}
    />
  );
}
```

#### `SponsorComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetSponsorStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsorStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetSponsorStyles` |

`SponsorComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetSponsor` component.

#### `BodyComponent`

| Type                                                                                                                        | Default                                                                                                   |
| :-------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| Component of type [LLAlertWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetBody) | [LLAlertWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetBody) |

Refer [LLVoteWidgetBody](react-native-llalertwidget#llalertwidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                     | Default                                                                                          |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLAlertWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLAlertWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLAlertWidgetBody` component.

***

## LLAlertWidgetBody

This is a body component for a alert widget responsible for rendering alert text, image and links.

### Hooks used by `LLAlertWidgetBody`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
- [useWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidget)

### `LLAlertWidgetBody` Props

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `onLinkPress`

| Type                  | Default    |
| :-------------------- | :--------- |
| ({url: string}) => void | No Default |

#### `styles`

| Type                                                                                                                                     | Default                                                                                           |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| Stylesheet of type [LLAlertWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLAlertWidgetBodyStyles`. |

`styles` prop that could be used to modify styles of `LLAlertWidgetBody` component.

#### `DetailComponent`

| Type                                                                                                                            | Default                                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------ |
| Component of type [LLAlertWidgetDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetDetail) | [LLAlertWidgetDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetDetail) |

Component responsible for rendering alert widget text (if present) and image (if present). 

#### `DetailComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLAlertWidgetDetailStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetDetailStyles) | No Default, if present styles props would be applied on top of internal `LLAlertWidgetDetailStyles` |

`DetailComponentStyles` prop that could be used to modify styles of default rendered `LLAlertWidgetDetail` component.

#### `LinkComponent`

| Type                                                                                                                            | Default                                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------ |
| Component of type [LLAlertWidgetLink](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetLink) | [LLAlertWidgetLink](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetLink) |

Component responsible for rendering alert widget link (if present). When user presses link, `onLinkPress` prop function gets invoked.

#### `LinkComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLAlertWidgetLinkStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidgetLinkStyles) | No Default, if present styles props would be applied on top of internal `LLAlertWidgetLinkStyles` |

`LinkComponentStyles` prop that could be used to modify styles of default rendered `LLAlertWidgetLink` component.