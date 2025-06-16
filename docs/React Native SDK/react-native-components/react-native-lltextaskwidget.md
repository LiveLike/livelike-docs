---
title: LLTextAskWidget
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

## LLTextAskWidget

`LLTextAskWidget` is a text input based widget UI component where it could be used to get information from your user.

```javascript react native
import { LLTextAskWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetContainer() {
  return (
    <LLTextAskWidget
      programId="xxxxx"
      widgetId="yyyyy"
    />
  );
}
```

### Hooks used by `LLTextAskWidget`

* [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)
* [useWidgetExpiryEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetExpiryEffect)

### LLTextAskWidget Props

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
import { LLTextAskWidget, LLWidgetHeaderProps } from '@livelike/react-native';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLTextAskWidget
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
import { LLTextAskWidget, LLWidgetFooterProps } from '@livelike/react-native';

function MyFooterComponent(props: LLWidgetFooterProps){
  // your custom widget footer component
}

function MyWidget() {
  return (
    <LLTextAskWidget
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

| Type                                                                                                                              | Default                                                                                                         |
| :-------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| Component of type [LLTextAskWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetBody) | [LLTextAskWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetBody) |

Refer [LLTextAskWidgetBody](react-native-lltextaskwidget#lltextaskwidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                           | Default                                                                                             |
| :--------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLTextAskWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLTextAskWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLTextAskWidgetBody` component.

***

## LLTextAskWidgetBody

This is a body component for a vote option based widget responsible for rendering all the option details and its interaction.

### Hooks used by `LLTextAskWidgetBody`

* [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
* [useWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidget)
* [useWidgetInteractions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractions)
* [useIsWidgetDisabled](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useIsWidgetDisabled)
* [useWidgetActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetActions)

### `LLTextAskWidgetBody` Props

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                           | Default                                                                                              |
| :--------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------- |
| Stylesheet of type [LLTextAskWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLTextAskWidgetBodyStyles`. |

`styles` prop that could be used to modify styles of `LLTextAskWidgetBody` component.

#### `InputComponent`

| Type                                                                                                                                | Default                                                                                                           |
| :---------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- |
| Component of type [LLTextAskWidgetInput](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetInput) | [LLTextAskWidgetInput](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidgetInput) |

Component responsible for rendering text input UI.

#### `InputComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetOptionStyles` |

`InputComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetVoteOption` component.
