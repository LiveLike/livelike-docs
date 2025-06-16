---
title: LLPredictionFollowUpWidget
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

## LLPredictionFollowUpWidget

`LLPredictionFollowUpWidget` is a prediction based non interact-able widget UI component. This widget UI supports two kinds of widget:

1. `WidgetKind.TEXT_PREDICTION_FOLLOW_UP`
2. `WidgetKind.IMAGE_PREDICTION_FOLLOW_UP`

```typescript react native
import { LLPredictionFollowUpWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetContainer() {
  return (
    <LLPredictionFollowUpWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_PREDICTION_FOLLOW_UP}
    />
  );
}
```

### Hooks used by `LLPredictionFollowUpWidget`

- [usePredictionClaimRewardEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=usePredictionClaimRewardEffect)
- [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)

### LLPredictionFollowUpWidget Props

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
import { LLPredictionFollowUpWidget, LLWidgetHeaderProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLPredictionFollowUpWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_PREDICTION_FOLLOW_UP}
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
import { LLPredictionFollowUpWidget, LLWidgetFooterProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyFooterComponent(props: LLWidgetFooterProps){
  // your custom widget footer component
}

function MyWidget() {
  return (
    <LLPredictionFollowUpWidget
      programId="xxxxx"
      widgetId="yyyyy"
      widgetKind={WidgetKind.IMAGE_PREDICTION_FOLLOW_UP}
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
| Component of type [LLVoteWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLVoteWidgetBody) | [LLVoteWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLVoteWidgetBody) |

Refer [LLVoteWidgetBody](react-native-llpredictionfollowupwidget#llvotewidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                     | Default                                                                                          |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLVoteWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLVoteWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLVoteWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLVoteWidgetBody` component.

***

## LLVoteWidgetBody

This is a body component for a vote option based widget responsible for rendering all the option details and its interaction.

### Hooks used by `LLVoteWidgetBody`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
- [useWidgetOptions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetOptions)
- [useWidgetActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetActions)

### `LLVoteWidgetBody` Props

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

#### `VoteOptionComponent`

| Type                                                                                                                            | Default                                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetVoteOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetVoteOption) | [LLWidgetVoteOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetVoteOption) |

Refer [LLWidgetVoteOption](react-native-llwidgetvoteoption) docs for more details.

#### `VoteOptionComponentStyles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOptionStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetOptionStyles` |

`VoteOptionComponentStyles` prop that could be used to modify styles of default rendered `LLWidgetVoteOption` component.