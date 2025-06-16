---
title: LLWidgets
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

`LLWidgets` is a timeline based widget container component that would render set of widgets based on `WidgetMode`  (`POPUP` or `INTERACTIVE_TIMELINE`) where the mode defines how those set of widgets (published from our producer suite) would be rendered.

Let us understand different types of widget mode.

### Popup Mode:

In popup mode (i.e `WidgetMode.POPUP`), widgets appear for a limited time and then disappear. They are interactive until the timer animation runs out. It is typically used for live interactive experiences.

```typescript react native
import { LLWidgets, WidgetMode } from '@livelike/react-native';

export function MyWidgetsContainer() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.POPUP}
    />
  );
}
```

### Interactive Timeline Mode:

In interactive timeline mode (i.e `WidgetMode.INTERACTIVE_TIMELINE`), 

- previously published widgets are displayed newest to oldest 
- then new widgets appear above the old ones. 
- All the widgets are interactive for infinite time. There is **no timer** attached to any of the widgets.  
- Each "page" of widgets in the timeline contain up to the 20 most recent widgets. 
- If there are more than 20 past widgets available, there will be a customisable "Load More" button at the end of the widget list that will load up to the next 20 widgets at a time.

```typescript react native
import { LLWidgets, WidgetMode } from '@livelike/react-native';

export function MyWidgetsContainer() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
    />
  );
}
```

> 📘 Snack expo playground
> 
> Refer [LLWidgets](https://snack.expo.dev/@aquibv/llwidgets) snack to play around with the widget

## Hooks used by `LLWidgets`

- [useLoadTimelineWidgetEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useLoadTimelineWidgetEffect)
- [useTimelineWidgets](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useTimelineWidgets)
- [useTimelineWidgetActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useTimelineWidgetActions)

## LLWidgets Props

> 📘 Customisation
> 
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation.

#### `programId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

This is the Id of the program in which a given set of  widgets are published from producer suite.

#### `mode`

| Type                                                                                                          | Default    |
| :------------------------------------------------------------------------------------------------------------ | :--------- |
| [WidgetMode](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=WidgetMode)  (**Required**) | No default |

This prop defines in which mode `LLWidgets` component to be rendered.

#### `styles`

| Type                                                                                                                       | Default                                                                                    |
| :------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------- |
| Stylesheet of type [LLWidgetsStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetsStyles) | No Default, if present styles props would be applied on top of internal `LLWidgetsStyles`. |

#### `onLoadMore`

| Type       | Default    |
| :--------- | :--------- |
| () => void | No default |

Function that called whenever more widgets are loaded in `interactive-timeline` mode.

#### `LoadingComponent`

| Type            | Default                                                                                          |
| :-------------- | :----------------------------------------------------------------------------------------------- |
| React Component | [ActivityIndicator](https://reactnative.dev/docs/activityindicator) as default Loading component |

Component to render whenever set of widgets are being loaded in `interactive-timeline` mode. 

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode } from '@livelike/react-native';
import { View, Text } from 'react-native';

const CustomLoadingComponent = () => {
  return (
		<View>
    	<Text> Loading... </Text>
    </View>
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
      LoadingComponent={CustomLoadingComponent}
    />
  );
}
```

#### `ErrorComponent`

| Type            | Default                                                             |
| :-------------- | :------------------------------------------------------------------ |
| React Component | View and Text component showing `Unable to load widgets` error text |

Component to render whenever there's an error in loading widgets in `interactive-timeline` mode. 

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode } from '@livelike/react-native';
import { View, Text } from 'react-native';

const CustomErrorComponent = () => {
  return (
		<View>
    	<Text style={{ color: 'red' }}> Ohh snap! widgets not loaded </Text>
    </View>
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
      ErrorComponent={CustomErrorComponent}
    />
  );
}
```

#### `LoadMoreComponent`

| Type                                                                                                                                      | Default                                                                                                                 |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| Component of type [LLWidgetsLoadMoreButton](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetsLoadMoreButton) | [LLWidgetsLoadMoreButton](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetsLoadMoreButton) |

Pressable component which when pressed loads next set of widgets in `interactive-timeline` mode.

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode, LLWidgetsLoadMoreButtonProps } from '@livelike/react-native';
import { Button } from 'react-native';

const CustomLoadMoreComponent = ({onPress}: LLWidgetsLoadMoreButtonProps) => {
  return (
    	<Button onPress={onPress}>Roll more widgets</Text>
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
      LoadMoreComponent={CustomLoadMoreComponent}
    />
  );
}
```

#### `LoadMoreComponentStyles`

| Type                                                                                                                                       | Default                                                                                           |
| :----------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| StyleSheet of type [LoadMoreComponentStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LoadMoreComponentStyles) | No Default, if present styles props would be applied on top of internal `LoadMoreComponentStyles` |

LoadMoreComponentStyles styles prop which could be used to modify styles of default rendered `LoadMoreComponent` component.

#### `WidgetSeparatorComponent`

| Type                                                                                                                           | Default                                                                                                     |
| :----------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| React component or [LLWidgetSeparator](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSeparator) | [LLWidgetSeparator](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidgetSeparator) |

Component to render between widgets (as a separator)

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode } from '@livelike/react-native';
import { View, Text } from 'react-native';

const CustomSeparatorComponent = () => {
  return (
		// your custom separator
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
      WidgetSeparatorComponent={CustomSeparatorComponent}
    />
  );
}
```

#### `WidgetSeparatorComponentStyles`

| Type                                                                                                                                                     | Default                                                                                                  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [WidgetSeparatorComponentStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=WidgetSeparatorComponentStyles) | No Default, if present styles props would be applied on top of internal `WidgetSeparatorComponentStyles` |

WidgetSeparatorComponentStyles styles prop which could be used to modify styles of default rendered `WidgetSeparatorComponent` component.

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode } from '@livelike/react-native';
import { View, Text } from 'react-native';

const CustomLoadingComponent = () => {
  return (
		<View>
    	<Text> Loading... </Text>
    </View>
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
			LoadingComponent={CustomLoadingComponent}
    />
  );
}
```

#### `WidgetComponent`

| Type                                                                                                              | Default                                                                                   |
| :---------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------- |
| React component of type [LLWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidget) | [LLWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLWidget) |

WidgetComponent is responsible for rendering widget UI based on its kind. Internally it render LiveLike stock UI [widgets](react-native-widget). You can pass a custom component to render your own widget UI or pass an extended LLWidget component customising a given set of widget kinds.

##### Example usage:

Render your own custom Alert widget or customise stock Poll widget. 

```typescript React Native
import React from 'react';
import { 
  LLWidgets,
  LLWidget,
  LLWidgetProps, 
  LLPollWidgetProps,
  LLWidgetHeaderProps,
  useWidget,
  WidgetMode
} from '@livelike/react-native';
import { View, Text } from 'react-native';

function CustomPollHeaderComponent(props: LLWidgetHeaderProps){
  return (
    // tour custom poll header UI
  )
}

function CustomPollComponent({ widgetId, ...rest }: LLPollWidgetProps){
  return (
  	<LLPollWidget
    	{...rest}
			widgetId={widgetId}
			HeaderComponent={CustomPollHeaderComponent}
    />
  ) 
}

function CustomAlertComponent({ widgetId }){
	const widgetDetails = useWidget({ widgetId });
  return (
     // your alert UI
  )
}

function CustomWidget(props: LLWidgetProps) {
  return <LLWidget
  				{...props} 
  				PollComponent={CustomPollComponent}
  				AlertComponent={CustomAlertComponent}
  			/>;
}

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
			WidgetComponent={CustomWidget}
    />
  );
}
```

# LLWidget

This component renders widget UI based on widget kind which is used by `LLWidgets` component. You can pass corresponding widget kind prop to render your own custom Widget UI.

## LLWidget Props:

#### `widgetKind`

| Type                                                                                                    | Default    |
| :------------------------------------------------------------------------------------------------------ | :--------- |
| [WidgetKind](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=WidgetKind) (**Required**) | No Default |

#### `PollWidgetComponent`

| Type                                                                                                                 | Default                                             |
| :------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------- |
| React component or [LLPollWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLPollWidget) | [LLPollWidget](react-native-llpollwidget) component |

Component rendered for text or image poll widget kind, you can pass your own custom component or pass a customised `LLPollWidget` component.

##### Example usage:

```typescript React Native
import React from 'react';
import { LLWidgets, WidgetMode } from '@livelike/react-native';
import { View, Text } from 'react-native';

const CustomLoadingComponent = () => {
  return (
		<View>
    	<Text> Loading... </Text>
    </View>
  );
};

export function MyApp() {
  return (
    <LLWidgets
      programId="xxxxx"
      mode={WidgetMode.INTERACTIVE_TIMELINE}
			LoadingComponent={CustomLoadingComponent}
    />
  );
}
```

#### `QuizWidgetComponent`

| Type                                                                                                                 | Default                                             |
| :------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------- |
| React component or [LLQuizWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLQuizWidget) | [LLQuizWidget](react-native-llquizwidget) component |

Component rendered for text or image quiz widget kind, you can pass your own custom component or pass a customised `LLQuizWidget` component.

#### `PredictionWidgetComponent`

| Type                                                                                                                             | Default                                                         |
| :------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- |
| React component or [LLPredictionWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLPredictionWidget) | [LLPredictionWidget](react-native-llpredictionwidget) component |

Component rendered for text or image prediction widget kind, you can pass your own custom component or pass a customised `LLPredictionWidget` component.

#### `PredictionFollowUpWidgetComponent`

| Type                                                                                                                                             | Default                                                                         |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------ |
| React component or [LLPredictionFollowUpWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLPredictionFollowUpWidget) | [LLPredictionFollowUpWidget](react-native-llpredictionfollowupwidget) component |

Component rendered for text or image prediction follow up widget kind, you can pass your own custom component or pass a customised `LLPredictionFollowUpWidget` component.

#### `NumberPredictionWidgetComponent`

| Type                                                                                                                                         | Default                                                                     |
| :------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| React component or [LLNumberPredictionWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLNumberPredictionWidget) | [LLNumberPredictionWidget](react-native-llnumberpredictionwidget) component |

Component rendered for text or image number prediction widget kind, you can pass your own custom component or pass a customised `LLNumberPredictionWidget` component.

#### `NumberPredictionFollowUpWidgetComponent`

| Type                                                                                                                                                         | Default                                                                                     |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------ |
| React component or [LLNumberPredictionFollowUpWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLNumberPredictionFollowUpWidget) | [LLNumberPredictionFollowUpWidget](react-native-llnumberpredictionfollowupwidget) component |

Component rendered for text or image number prediction follow up widget kind, you can pass your own custom component or pass a customised `LLNumberPredictionFollowUpWidget` component.

#### `EmojiSliderWidgetComponent`

| Type                                                                                                                               | Default                                                           |
| :--------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| React component or [LLEmojiSliderWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLEmojiSliderWidget) | [LLEmojiSliderWidget](react-native-llemojisliderwidget) component |

Component rendered for emoji slider widget kind, you can pass your own custom component or pass a customised `LLEmojiSliderWidget` component.

#### `CheerMeterWidgetComponent`

| Type                                                                                                                             | Default                                                         |
| :------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- |
| React component or [LLCheerMeterWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLCheerMeterWidget) | [LLCheerMeterWidget](react-native-llcheermeterwidget) component |

Component rendered for cheer meter widget kind, you can pass your own custom component or pass a customised `LLEmojiSliderWidget` component.

#### `TextAskComponent`

| Type                                                                                                                       | Default                                                   |
| :------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------- |
| React component or [LLTextAskWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTextAskWidget) | [LLTextAskWidget](react-native-lltextaskwidget) component |

Component that could be rendered for text ask widget kind, you can pass your own custom component or pass a customised `LLTextAskWidget` component.

#### `AlertComponent`

| Type                                                                                                                   | Default                                               |
| :--------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------- |
| React component or [LLAlertWidget](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLAlertWidget) | [LLAlertWidget](react-native-llalertwidget) component |

Component that could be rendered for alert widget kind, you can pass your own custom component or pass a customised `LLAlertWidget` component.

#### `VideoAlertComponent`

| Type            | Default                       |
| :-------------- | :---------------------------- |
| React component | By default, no UI is rendered |

Component that could be rendered for video alert widget kind, you can pass your own custom component.

#### `SocialEmbedComponent`

| Type            | Default                       |
| :-------------- | :---------------------------- |
| React component | By default, no UI is rendered |

Component that could be rendered for social embed widget kind, you can pass your own custom component.

> 🚧 Widgets in development
> 
> Currently text ask, alert, video alert and social embed stock widget UI is in development. So by default there's no stock widget UI rendered by LLTimelineWidget.