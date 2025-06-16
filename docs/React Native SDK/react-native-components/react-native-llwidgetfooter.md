---
title: LLWidgetFooter
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
        "https://files.readme.io/6d31b37-Group_69.svg",
        null,
        "Widget footer Anatomy"
      ],
      "align": "center",
      "sizing": "750px",
      "caption": "Widget Footer Anatomy"
    }
  ]
}
[/block]

`LLWidgetFooter` is a fundamental atomic component that is used by various widget components. This component is rendered as a bottom component as part of default [widget anatomy](react-native-widget-anatomy).

```typescript react native
import { LLWidgetFooter } from '@livelike/react-native';

export function MyWidgetFooter() {
  return (
    <LLWidgetFooter
      widgetId="yyyyy"
    />
  );
}
```

## Hooks used by `LLWidgetFooter`

- [useWidgetInteractiveTimeout](react-native-usewidgetinteractivetimeout)
- [useWidgetExpiryEffect](react-native-usewidgetexpiryeffect)

## Component Hierarchy

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/abe87fd-Widget_Doc-Component_hierarchy.drawio_2.svg",
        null,
        "Footer component hierarchy"
      ],
      "align": "center"
    }
  ]
}
[/block]

## LLWidgetFooter Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                 | Default                                                                                        |
| :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetFooterStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetFooterStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetFooterStyles` |

#### `ActionInfoComponent`

| Type                                                                                                                            | Default                                                                                                       |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetActionInfo](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetActionInfo) | [LLWidgetActionInfo](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetActionInfo) |

Renders widget action related components that comprises of:

- End phase label i.e Timed Out | Expired
- Rewards earned by user.
- submit button for single interaction based widgets.

Pass your own custom action info component or extend default LLWidgetActionInfo stock component by customising above sub components.  
Refer [LLWidgetActionInfo](react-native-llwidgetfooter#llwidgetactioninfo) for more details.   

##### Example usage:

```typescript React Native
import { LLWidgetFooter, LLWidgetActionInfoProps } from '@livelike/react-native';

// Widget footer with custom action info component

function MyActionInfoComponent(props: LLWidgetActionInfoProps){
  // your own custom action info implementation
  // you could reuse stock sub components and create your own container UI
}

export function MyWidgetFooter() {
  return (
    <LLWidgetFooter
      widgetId="yyyyy"
      ActionInfoComponent={MyActionInfoComponent}
    />
  );
}
```

#### `ActionInfoComponentStyles`

| Type                                                                                                                                         | Default                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetActionInfoStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetActionInfoStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetActionInfoStyles` |

`ActionInfoComponentStyles` prop which could be used to modify styles of default rendered `LLWidgetActionInfo` component.

#### `SponsorComponent`

| Type                                                                                                                      | Default                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetSponsor](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsor) | [LLWidgetSponsor](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsor) |

Renders sponsor component based on the sponsor selected for a given widget through our producer suite.   

##### Example usage:

```typescript React Native
import { LLWidgetFooter, LLWidgetSponsorProps } from '@livelike/react-native';

// Widget footer with custom action info component

function MySponsorComponent(props: LLWidgetSponsorProps){
  // your own custom sponsor component implementation
}

export function MyWidgetFooter() {
  return (
    <LLWidgetFooter
      widgetId="yyyyy"
      SponsorComponent={MySponsorComponent}
    />
  );
}
```

#### `SponsorComponentStyles`

| Type                                                                                                                                   | Default                                                                                         |
| :------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetSponsorStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSponsorStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetSponsorStyles` |

`LLWidgetSponsorStyles` prop which could be used to modify styles of default rendered `LLWidgetSponsor` component.

***

## LLWidgetActionInfo

Renders widget action related components that comprises of:

- End phase label i.e Timed Out | Expired
- Rewards earned by user.
- submit button for single interaction based widgets.

### Hooks used by `LLWidgetActionInfo`

- [useStyles](react-native-usestyles)

### LLWidgetActionInfo Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `widgetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `styles`

| Type                                                                                                                                         | Default                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetActionInfoStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetActionInfoStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetActionInfoStyles` |

#### `EndWidgetUIPhaseLabelComponent`

| Type                                                                                                                                      | Default                                                                                                                 |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| Component of type [LLEndWidgetUIPhaseLabel](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEndWidgetUIPhaseLabel) | [LLEndWidgetUIPhaseLabel](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEndWidgetUIPhaseLabel) |

Renders end phase label when widget is in either **Timed out** or **Expired** phase.

##### Example usage:

```typescript React Native
import { LLWidgetActionInfo, LLEndWidgetUIPhaseLabelProps } from '@livelike/react-native';

function MyEndPhaseUILabelComponent(props: LLEndWidgetUIPhaseLabelProps){
  // your own custom implementation
}

export function MyFooterActionInfo() {
  return (
    <LLWidgetActionInfo
      widgetId="yyyyy"
      EndWidgetUIPhaseLabelComponent={MyEndPhaseUILabelComponent}
    />
  );
}
```

#### `EndWidgetUIPhaseLabelComponentStyles`

| Type                                                                                                                                                   | Default                                                                                                 |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| StyleSheet of type [LLEndWidgetUIPhaseLabelStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEndWidgetUIPhaseLabelStyles) | No Default, if present styles props would be applied on top of internal `LLEndWidgetUIPhaseLabelStyles` |

`EndWidgetUIPhaseLabelComponentStyles` prop which could be used to modify styles of default rendered `LLEndWidgetUIPhaseLabel` component.

#### `WidgetRewardsComponent`

| Type                                                                                                                      | Default                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ |
| Component of type [LLWidgetRewards](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetRewards) | [LLWidgetRewards](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetRewards) |

Render rewards earned based on user interaction provided reward has been setup for a given widget through producer suite. In case of multiple rewards earned, reward items are animated using slides in and out transition.  

##### Example usage:

```typescript React Native
import { 
  LLWidgetActionInfo,
  LLWidgetRewards,
  LLWidgetRewardsProps
} from '@livelike/react-native';

function MyRewardsComponent(props: LLWidgetRewardsProps){
  // your own custom implementation
  // or extend stock rewards component
  return <LLWidgetRewards
    {...props}
    // customise reward item component
    RewardComponent={LLWidgetReward}
    // customise reward item styles
    RewardComponentStyles={<custom stylesheet of type LLWidgetRewardStyles>}
  />
}

export function MyFooterActionInfo() {
  return (
    <LLWidgetActionInfo
      widgetId="yyyyy"
      WidgetRewardsComponent={MyRewardsComponent}
    />
  );
}
```

#### `WidgetRewardsComponentStyles`

| Type                                                                                                                                   | Default                                                                                         |
| :------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetRewardsStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetRewardsStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetRewardsStyles` |

`WidgetRewardsComponentStyles` prop which could be used to modify styles of default rendered `LLWidgetRewards` component.

#### `SubmitButtonComponent`

| Type                                                                                                                                               | Default                                |
| :------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------- |
| Component of type Prop [LLWidgetSubmitButtonProps](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSubmitButtonProps) | By default there no component rendered |

Renders submit button component by a given widget whose on Submit behaviour is defined by corresponding widget.

##### Example usage:

```typescript React Native
import { LLWidgetActionInfo, LLWidgetSubmitButtonProps } from '@livelike/react-native';

function MySubmitComponent(props: LLWidgetSubmitButtonProps){
  // your own custom implementation
  // or extend stock LLWidgetSubmitButtonComponent
}

export function MyFooterSubmit() {
  return (
    <LLWidgetActionInfo
      widgetId="yyyyy"
      SubmitButtonComponent={MySubmitComponent}
    />
  );
}
```

#### `SubmitButtonComponentStyles`

| Type                                                                                                                                             | Default                                                                                              |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLWidgetSubmitButtonStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSubmitButtonStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetSubmitButtonStyles` |

`SubmitButtonComponentStyles` prop which could be used to modify styles of default rendered `SubmitButtonComponent` component.