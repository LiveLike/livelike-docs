---
title: LLQuizWidget
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

## LLQuizWidget

`LLQuizWidget` is a quiz based widget UI component. This widget UI supports two kinds of widget:

1. `WidgetKind.TEXT_QUIZ`
2. `WidgetKind.IMAGE_QUIZ`

```typescript react native
import { LLQuizWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetContainer() {
  return (
    <LLQuizWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_QUIZ}
    />
  );
}
```

### Hooks used by `LLQuizWidget`

- [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)
- [useWidgetExpiryEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetExpiryEffect)

### LLQuizWidget Props

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

#### `widgetKind`

| Type                                                                                                    | Default    |
| :------------------------------------------------------------------------------------------------------ | :--------- |
| [WidgetKind](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=WidgetKind) (**Required**) | No Default |

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
import { LLQuizWidget, LLWidgetHeaderProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLQuizWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_QUIZ}
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
import { LLQuizWidget, LLWidgetFooterProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyFooterComponent(props: LLWidgetFooterProps){
  // your custom widget footer component
}

function MyWidget() {
  return (
    <LLQuizWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_QUIZ}
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

| Type                                                                                                                        | Default                                                                                                   |
| :-------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| Component of type [LLQuizWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLQuizWidgetBody) | [LLQuizWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLQuizWidgetBody) |

Refer [LLQuizWidgetBody](react-native-llquizwidget#llquizwidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                     | Default                                                                                          |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLQuizWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLQuizWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLQuizWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLQuizWidgetBody` component.

***

## LLQuizWidgetBody

This is a body component for a quiz widget responsible for rendering quiz choice details and its interaction.

### Hooks used by `LLQuizWidgetBody`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
- [useWidgetChoices](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetChoices)
- [useWidgetActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetActions)

### `LLQuizWidgetBody` Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                     | Default                                                                                           |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| Stylesheet of type [LLVoteWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLVoteWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLVoteWidgetBodyStyles`. |

`styles` prop that could be used to modify styles of `LLVoteWidgetBody` component.

#### `ChoiceOptionComponent`

| Type                                                                                                                                | Default                                                                                                           |
| :---------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetChoiceOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetChoiceOption) | [LLWidgetChoiceOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetChoiceOption) |

Refer [LLWidgetChoiceOption](react-native-llquizwidget#llwidgetchoiceoption)in below section for more details.

#### `ChoiceOptionComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetOptionStyles` |

`ChoiceOptionComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetChoiceOption` component.

***

## LLWidgetChoiceOption

`LLWidgetChoiceOption` is a container component that renders quiz widget choice option using [LLWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOption) as its presentational component. It derives all the choice details and interaction handler needed by `LLWidgetOption` component.  

### Hooks used by `LLWidgetChoiceOption`

- [useWidgetResultState](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetResultState)
- [useWidgetChoices](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetChoices)
- [useInteractedWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useInteractedWidgetOption)
- [useIsWidgetOptionDisabled](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useIsWidgetOptionDisabled)

### LLWidgetChoiceOption Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `optionIndex`

| Type                  | Default    |
| :-------------------- | :--------- |
| Number (**Required**) | No Default |

Index of the widget option

#### `selectedOptionIndex`

| Type                  | Default                         |
| :-------------------- | :------------------------------ |
| Number (**Required**) | `-1` when no option is selected |

Index of the selected widget option

#### `onOptionChange`

| Type                           | Default    |
| :----------------------------- | :--------- |
| (optionIndex: number) => void; | No Default |

Function that gets invoked with option index whenever vote option is selected.

#### `OptionComponent`

| Type                                                                                                                    | Default                                                                                               |
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOption) | [LLWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOption) |

Presentational component for option component. 

#### `OptionComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetOptionStyles` |

`OptionComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetOption` component.