---
title: LLEmojiSliderWidget
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

## LLEmojiSliderWidget

`LLEmojiSliderWidget` is a slider based widget UI component.

```typescript react native
import { LLEmojiSliderWidget } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

export function MyWidgetContainer() {
  return (
    <LLEmojiSliderWidget
      programId="xxxxx"
      widgetId="yyyyy"
    />
  );
}
```

### Hooks used by `LLEmojiSliderWidget`

- [useWidgetInteractiveTimeout](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractiveTimeout)
- [useWidgetExpiryEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetExpiryEffect)

### LLEmojiSliderWidget Props

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
import { LLEmojiSliderWidget, LLWidgetHeaderProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyHeaderComponent(props: LLWidgetHeaderProps){
  // your custom widget header component
}

function MyWidget() {
  return (
    <LLEmojiSliderWidget
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
import { LLEmojiSliderWidget, LLWidgetFooterProps } from '@livelike/react-native';
import { WidgetKind } from '@livelike/javascript';

function MyFooterComponent(props: LLWidgetFooterProps){
  // your custom widget footer component
}

function MyWidget() {
  return (
    <LLEmojiSliderWidget
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

| Type                                                                                                                                      | Default                                                                                                                 |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| Component of type [LLEmojiSliderWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderWidgetBody) | [LLEmojiSliderWidgetBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderWidgetBody) |

Refer [LLEmojiSliderWidgetBody](react-native-llemojisliderwidget#llemojisliderwidgetbody) in below section for more details. 

#### `BodyComponentStyles`

| Type                                                                                                                                                   | Default                                                                                                 |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| StyleSheet of type [LLEmojiSliderWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLEmojiSliderWidgetBodyStyles` |

`BodyComponentStyles` prop that could be used to modify styles of default rendered `LLEmojiSliderWidgetBody` component.

***

## LLEmojiSliderWidgetBody

This is a body component for a emoji slider widget responsible for rendering slider and its interaction.

### Hooks used by `LLEmojiSliderWidgetBody`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
- [useWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidget)
- [useWidgetOptions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetOptions)
- [useWidgetActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetActions)
- [useIsWidgetDisabled](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useIsWidgetDisabled)
- [useWidgetInteractions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useWidgetInteractions)

### `LLEmojiSliderWidgetBody` Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                                   | Default                                                                                                  |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| Stylesheet of type [LLEmojiSliderWidgetBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderWidgetBodyStyles) | No Default, if present styles props would be applied on top of internal `LLEmojiSliderWidgetBodyStyles`. |

`styles` prop that could be used to modify styles of `LLEmojiSliderWidgetBody` component.

#### `SliderComponent`

| Type                                                                                                                  | Default                                                                                             |
| :-------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| Component of type [LLEmojiSlider](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSlider) | [LLEmojiSlider](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSlider) |

Refer [LLEmojiSlider](react-native-llemojisliderwidget#llemojislider) in below section for more details.

#### `SliderComponentStyles`

| Type                                                                                                                               | Default                                                                                       |
| :--------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLEmojiSliderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderStyles) | No Default, if present styles props would be applied on top of internal `LLEmojiSliderStyles` |

`SliderComponentStyles` prop that could be used to modify styles of default rendered `LLEmojiSlider` component.

## LLEmojiSlider

This is the slider component for a emoji slider widget responsible for rendering slider UI. Internally it renders [react-native-slider](https://github.com/miblanchard/react-native-slider) 

### Hooks used by `LLEmojiSlider`

- [useStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useStyles)
- [useEmojiSlider](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useEmojiSlider)

### `LLEmojiSlider` Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `onSlidingComplete`

| Type                                   | Default    |
| :------------------------------------- | :--------- |
| (value: number) => void (**Required**) | No Default |

Function called with sliding input value when user sliding interaction is completed.

#### `thumbImages`

| Type                                                    | Default    |
| :------------------------------------------------------ | :--------- |
| Array of {min: number; imageUrl: string} (**Required**) | No Default |

Array of thump images to be shown for a given value range of sliding input 

#### `value`

| Type                  | Default    |
| :-------------------- | :--------- |
| Number (**Required**) | No Default |

Current value of the sliding UI input. 

#### `initialValue`

| Type   | Default    |
| :----- | :--------- |
| Number | No Default |

Initial value of the sliding UI input.

#### `average`

| Type   | Default    |
| :----- | :--------- |
| Number | No Default |

Average value of all the user interaction done so far on a given slider UI.

#### `disabled`

| Type    | Default |
| :------ | :------ |
| boolean | `false` |

#### `styles`

| Type                                                                                                                               | Default                                                                                        |
| :--------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| Stylesheet of type [LLEmojiSliderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderStyles) | No Default, if present styles props would be applied on top of internal `LLEmojiSliderStyles`. |

`styles` prop that could be used to modify styles of `LLEmojiSlider` component.

#### `sliderUIComponentProps`

| Type                                                                                           | Default    |
| :--------------------------------------------------------------------------------------------- | :--------- |
| slider props of type [react-native-slider](https://github.com/miblanchard/react-native-slider) | No Default |

Extend or customise internal slider UI component using `sliderUIComponentProps`, refer [react-native-slider](https://github.com/miblanchard/react-native-slider) supported props for more details.