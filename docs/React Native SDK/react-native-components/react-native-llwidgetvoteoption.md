---
title: LLWidgetVoteOption
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
`LLWidgetVoteOption` is a container component that renders a vote based widget option details using [LLWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetOption) as its presentational component. It derives all the option details and interaction handler needed by `LLWidgetOption` component.  
This widget is used by:

- [LLPollWidget](react-native-llpollwidget)
- [LLPredictionWidget](react-native-llpredictionwidget)
- [LLPredictionFollowUpWidget](react-native-llpredictionfollowupwidget)

## Hooks used by `LLWidgetVoteOption`

- [useWidgetInteractionActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractionActions)
- [useWidgetResultState](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetResultState)
- [useWidgetOptions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetOptions)
- [useInteractedWidgetOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useInteractedWidgetOption)
- [useIsWidgetOptionDisabled](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useIsWidgetOptionDisabled)

## LLWidgetVoteOption Props

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

#### `correctable`

| Type    | Default |
| :------ | :------ |
| Boolean | false   |

Specify whether a widget option is correctable i.e show a green border for a correct option or red border for an incorrect option. Used by Prediction follow up widget.

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