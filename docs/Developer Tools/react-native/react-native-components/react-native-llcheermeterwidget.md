---
title: LLCheerMeterWidget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Cheer Meter Widget | React Native SDK | LiveLike Developer Hub
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Pre-requisite
>
> Make sure you [initialise React Native SDK](react-native-getting-started#initialise-react-native-sdk).

## LLCheerMeterWidget

`LLCheerMeterWidget` is a cheer meter based widget UI component that could be used by your users to root for their favourable teams, players, tournaments, etc.

> 📘 Snack expo playground
>
> Refer [LLCheerMeterWidget](https://snack.expo.dev/@aquibv/llcheermeterwidget) snack to play around with the widget

```typescript react native
import { LLCheerMeterWidget } from '@livelike/react-native';

export function MyWidgetContainer() {
  return (
    <LLCheerMeterWidget
      programId="xxxxx"
      widgetId="yyyyy"
    />
  );
}
```

### Hooks used by `LLCheerMeterWidget`

* [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)
* [useWidgetExpiryEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetExpiryEffect)

### LLCheerMeterWidget Props

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

Function that gets invoked whenever user dismisses the widget by clicking on dismiss Icon.\
Pass `onDismiss` prop (with no op function) to make widget `dismissible`.

#### `interactiveTimeout`

| Type   | Default    |
| :----- | :--------- |
| Number | No default |

Interactive timeout in [epoch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_epoch_timestamps_and_invalid_date). Once the timeout gets elapsed, widget transition into `Timed Out` phase where it is in disabled state.\
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

This is the core widget component that is responsible for loading widget details and rendering other part of widget UI (passed as children).\
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
import { LLCheerMeterWidget, LLWidgetHeaderProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLCheerMeterWidget
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

#### `FooterComponent`

| Type                                                                                                                    | Default                                                                                               |
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetFooter](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetFooter) | [LLWidgetFooter](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetFooter) |

Refer [LLWidgetFooter](react-native-llwidgetfooter) docs for more details.

##### Example usage:

```typescript React Native
import { LLCheerMeterWidget, LLWidgetFooterProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyFooterComponent(props: LLWidgetFooterProps){
  // your custom widget footer component
}

function MyWidget() {
  return (
    <LLCheerMeterWidget
      programId="xxxxx"
      widgetId="yyyyy"
      FooterComponent={MyFooterComponent}
    />
  );
}
```

#### `FooterComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetFooterStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetFooterStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetFooterStyles` |

`FooterComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetHeader` component.

#### `BodyComponent`

| Type                                                                                                                                    | Default                                                                                                               |
| :-------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------- |
| Component of type [LLCheerMeterWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetBody) | [LLCheerMeterWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetBody) |

Refer [LLCheerMeterWidgetBody](react-native-llcheermeterwidget#llcheermeterwidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                                 | Default                                                                                                |
| :--------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLCheerMeterWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLCheerMeterWidgetBody` component.

***

## LLCheerMeterWidgetBody

This is a body component for a cheer meter widget responsible for rendering cheer meter results, option details and its interaction.

### Hooks used by `LLCheerMeterWidgetBody`

* [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
* [useWidgetOptions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetOptions)

### `LLCheerMeterWidgetBody` Props

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                                 | Default                                                                                                 |
| :--------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| Stylesheet of type [LLCheerMeterWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetBodyStyles`. |

`styles` prop that could be used to modify styles of `LLCheerMeterWidgetBody` component.

#### `OptionComponent`

| Type                                                                                                                                        | Default                                                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| Component of type [LLCheerMeterWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetOption) | [LLCheerMeterWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetOption) |

Refer [LLCheerMeterWidgetOption](react-native-llcheermeterwidget#llcheermeterwidgetoption) in below section for more details.

#### `OptionComponentStyles`

| Type                                                                                                                                                     | Default                                                                                                  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLCheerMeterWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetOptionStyles` |

`OptionComponentStyles` prop that could be used to modify styles of default rendered `LLCheerMeterWidgetOption` component.

#### `ResultComponent`

| Type                                                                                                                                        | Default                                                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| Component of type [LLCheerMeterWidgetResult](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetResult) | [LLCheerMeterWidgetResult](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetResult) |

This component is responsible for rendering each option total cheer count. 

#### `ResultComponentStyles`

| Type                                                                                                                                                     | Default                                                                                                  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLCheerMeterWidgetResultStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetResultStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetResultStyles` |

`ResultComponentStyles` prop that could be used to modify styles of default rendered `LLCheerMeterWidgetResult` component.

#### `CheerCountComponent`

| Type                                                                                                                                                | Default                                                                                                                           |
| :-------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| Component of type [LLCheerMeterWidgetCheerCount](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetCheerCount) | [LLCheerMeterWidgetCheerCount](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetCheerCount) |

This component is responsible for rendering total cheers count. 

#### `CheerCountComponentStyles`

| Type                                                                                                                                                             | Default                                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLCheerMeterWidgetCheerCountStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetCheerCountStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetCheerCountStyles` |

`CheerCountComponentStyles` prop that could be used to modify styles of default rendered `LLCheerMeterWidgetCheerCount` component.

***

## LLCheerMeterWidgetOption

This is option component for a cheer meter widget responsible for rendering cheer meter option and its interaction.

### Hooks used by `LLCheerMeterWidgetOption`

* [useTheme](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useTheme)
* [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
* [useWidgetOptions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetOptions)
* [useIsWidgetDisabled](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useIsWidgetDisabled)
* [useCheerMeterOnOptionPress](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useCheerMeterOnOptionPress)

### `LLCheerMeterWidgetOption` Props

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `optionIndex`

| Type                  | Default    |
| :-------------------- | :--------- |
| Number (**Required**) | No Default |

Index of the option from the option array in widget details (that is `options` in [IWidgetPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetPayload))

#### `throttleTime`

| Type   | Default |
| :----- | :------ |
| Number | 3000    |

throttle time in milliseconds used to throttle update interaction calls whenever user keeps on cheering by continuously pressing widget option.

#### `styles`

| Type                                                                                                                                                     | Default                                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| Stylesheet of type [LLCheerMeterWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLCheerMeterWidgetOptionStyles`. |

`styles` prop that could be used to modify styles of `LLCheerMeterWidgetOption` component.
