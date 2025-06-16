---
title: Widget Apis
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget APIs | Android SDK | LiveLike
  description: >-
    Build custom experiences and widget workflows, including skipping
    interactions directly to results and controlling interaction durations.
    Enhance your app with powerful integration tools.
  robots: index
next:
  description: ''
---
This API allows integrators to build their own custom experiences or widget workflows like Skipping the interaction directly to results, controlling the interaction duration, etc.

We have a widget lifecycle listener contract which has all lifecycle related events and states.

```kotlin
abstract class WidgetLifeCycleEventsListener {

    abstract fun onWidgetPresented(widgetData: LiveLikeWidgetEntity)
    abstract fun onWidgetInteractionCompleted(widgetData: LiveLikeWidgetEntity)
    abstract fun onWidgetDismissed(widgetData: LiveLikeWidgetEntity)
    abstract fun onWidgetStateChange(state: WidgetStates, widgetData: LiveLikeWidgetEntity)
    abstract fun onUserInteract(widgetData: LiveLikeWidgetEntity)
}
```
```java
public abstract class WidgetLifeCycleEventsListener {
   public abstract void onWidgetPresented(@NotNull LiveLikeWidgetEntity var1);

   public abstract void onWidgetInteractionCompleted(@NotNull LiveLikeWidgetEntity var1);

   public abstract void onWidgetDismissed(@NotNull LiveLikeWidgetEntity var1);

   public abstract void onWidgetStateChange(@NotNull WidgetStates var1, @NotNull LiveLikeWidgetEntity var2);
}
```

## On Demand Widget Instantiation

This api allows to load widget directly from widget payload json recieved via rest apis or on pubnub subscriptions.  

```kotlin
liveLikeWidgetView.displayWidget(sdk, widgetJsonObject)
```
```java
liveLikeWidgetView.displayWidget(sdk, widgetJsonObject);
```

## Subscribing to Realtime Widgets

Using the widgetView you can subscribe to the upcoming new widgets that are published by the producer. 

> 🚧 Deprecated!
> 
> Use the widgetStream inside content session, to subscribe to the widgets published real time.

Implement the setWidgetListener method in widgetView.  
**Note**: Make sure to setSession in widgetView.

```kotlin
widget_view.setWidgetListener(object : WidgetListener {
                override fun onNewWidget(liveLikeWidget: LiveLikeWidget) {
                    //livelikeWidget
                }
            })
```
```java
widget_view.setWidgetListener(new WidgetListener() {
            @Override
            public void onNewWidget(@NotNull LiveLikeWidget liveLikeWidget) {
                //livelikeWidget                                              
            }
        });
```

Subscribe to the widgetStream in content session for real time widgets. You need to have the session set.

```kotlin
contentSession.widgetStream.subscribe(this) {
            it?.let {
                //Widget received realtime
            }
        }
```

## Get Published Widgets

Using a Content Session you can retrieve a paginated list of Widgets (up to 20 per page) that have already been published using the getPublishedWidgets method. You can pass `LivelikePagination.first` or `LivelikePagination.next` enum. 

`LivelikePagination.first` will always return the newest Widgets.  
`LivelikePagination..next` will return the next page from the oldest page loaded.  
If the result and error are both null that means the user reached the list end.

```kotlin
session.getPublishedWidgets(LiveLikePagination.FIRST,
                                    object : LiveLikeCallback<List<LiveLikeWidget?>>() {
                                        override fun onResponse(
                                            result: List<LiveLikeWidget?>?,
                                            error: String?
                                        ) {
                                           
                                        }
                                    })
```
```java
session.getPublishedWidgets(LiveLikePagination.FIRST,
                                    new LiveLikeCallback<List<LiveLikeWidget>>() {
                                       @Override 
                                       void onResponse(
                                            List<LiveLikeWidget> result,
                                            String error
                                        ) {
                                           
                                        }
                                    })
```

## Get Details of Published Widget

As an integrator, you have the ability to query our backend for a specific widget to either display it to the user right away or save the widget details for later use. In order to retrieve a Widget, you will need to know it's id and kind 

```kotlin
sdk.fetchWidgetDetails(
                    widgetId!!,
                    widgetKind!!, 
  object : LiveLikeCallback<LiveLikeWidget>() {
                        override fun onResponse(livelikeWidget: LiveLikeWidget?, error: String?) {
                            livelikeWidget?.let {
                                //widget detail
                            }
                          error?.let{
                            showError(error)//error fetching details
                        }
                    }
                )
```
```java
sdk.fetchWidgetDetails(
                widget.id,
                widget.kind, new LiveLikeCallback<LiveLikeWidget>() {
                    @Override
                    public void onResponse(@Nullable LiveLikeWidget result, @Nullable String error) {
                        result ?.let {
                            //widget detail
                        }
                        error ?.let {
                            showError(error)//error fetching details
                        }
                    }
                }
        );
```

## Get Widgets by specified criteria

Using a Content Session you can retrieve a paginated list of Widgets (up to 20 per page) using the getWidgets method. You can pass `LivelikePagination.first` or `LivelikePagination.next` enum. 

`LivelikePagination.first` will always return the newest Widgets.  
`LivelikePagination.next` will return the next page from the oldest page loaded.  
If the result and error are both null that means the user reached the list end.

`WidgetsRequestParameters` is used to filter widgets based on filtering options.  
 The filtering options include::

- widgetTypeFilter - The set of widget kinds to include 
- widgetStatus - The publishing status of the widget
- widgetOrdering - The order in which the widgets will be returned
- interactive - Filters for only widgets that can still be interacted with
- since - A Date parameter that filters out widgets with an earlier created date

```kotlin
session.getWidgets(
                LiveLikePagination.FIRST,
                WidgetsRequestParameters(
                    widgetTypeFilter = setOf(
                        WidgetType.IMAGE_PREDICTION_FOLLOW_UP,
                        WidgetType.IMAGE_PREDICTION
                    ),
                    widgetStatus = WidgetStatus.SCHEDULED,
                    ordering = WidgetsRequestOrdering.RECENT,
                    interactive = true 
                ),
                object : LiveLikeCallback<List<LiveLikeWidget>>() {
                    override fun onResponse(result: List<LiveLikeWidget>?, error: String?) {
                    ...
                    }
                }
            )
```
```java
session.getWidgets(
                LiveLikePagination.FIRST,
                new WidgetsRequestParameters(
                        new HashSet(Arrays.asList(
                                WidgetType.IMAGE_PREDICTION_FOLLOW_UP,
                                WidgetType.IMAGE_PREDICTION
                        )),
                        WidgetStatus.SCHEDULED,
                        WidgetsRequestOrdering.RECENT
                ),
                new LiveLikeCallback<List<LiveLikeWidget>>() {
                    @Override
                    public void onResponse(@Nullable List<LiveLikeWidget> result, @Nullable String error) {
                        ...
                    }
                }
        );
```

## Instantiate Widget From Widget Object

If you are getting the livelike widget object from our method(fetchWidgetDetails) then you can use it to show in the widgetView by using the method displayWidget.

```kotlin
widget_view.displayWidget( sdk,livelikeWidget )
```
```java
widget_view.displayWidget( sdk,livelikeWidget );
```

> 📘 current widget removal
> 
> 1. widgetView.clearWidget() allows to remove the current loaded widget.
> 2. Also If we reload the same widget view with another JSON previous one will get removed.

## Controlling widget state transitions

Currently, the widget has 4 states : 

1. **Ready** - Widget enters into this state When a widget is rendered completely 

![](https://files.readme.io/eff1886-state1.gif "state1.gif")

2. **Interacting** - Widget entering this state unlocks for interaction.

![](https://files.readme.io/7fc1fb1-state2.gif "state2.gif")

3. **Results** - Widget in this state show continuous voting results if any

4. **Finished** - Widget in this state generally considered as dead, no updates in this state.

![](https://files.readme.io/e94c2cd-state3.gif "state3.gif")

We have to disable the default widget state transition to take control by setting boolean `enableDefaultWidgetTransition` to false.

widgetView.moveToNextState() method is used to move to next state.

```kotlin
widgetView.enableDefaultWidgetTransition = false
        widgetView.widgetLifeCycleEventsListener = object : WidgetLifeCycleEventsListener() {
            override fun onWidgetPresented(widgetData: LiveLikeWidgetEntity) {
            }

            override fun onWidgetInteractionCompleted(widgetData: LiveLikeWidgetEntity) {
            }

            override fun onWidgetDismissed(widgetData: LiveLikeWidgetEntity) {
            }
          
           override fun onUserInteract(widgetData: LiveLikeWidgetEntity) {
						}

            override fun onWidgetStateChange(
                widgetStates: WidgetStates,
                widgetData: LiveLikeWidgetEntity
            ) {
                when (widgetStates) {
                    WidgetStates.READY -> {
                        // it is called when widget is rendered and gets ready
                        // interaction is locked in this state
                        // call moveToNextState to enter into ineraction state
                       widgetView. moveToNextState()
                    }
                    WidgetStates.INTERACTING -> {
                      delay(10000)//10 seconds
                      widgetView. moveToNextState()
                    }
                    WidgetStates.RESULTS -> {
                      delay(5)//5 seconds
                      widgetView. moveToNextState()
                    }
                    WidgetStates.FINISHED -> {
                      // we can call clearWidget() to remove current widget
                      // or keep it in finished state to build timeline mode
                    }
                }
            }
        }
```
```java
widgetView.setEnableDefaultWidgetTransition(false);
      widgetView.setWidgetLifeCycleEventsListener((WidgetLifeCycleEventsListener)(new WidgetLifeCycleEventsListener() {
         public void onWidgetPresented(@NotNull LiveLikeWidgetEntity widgetData) {
             // it is called when widget is rendered and gets ready
                        // interaction is locked in this state
                        // call moveToNextState to enter into ineraction state
                       widgetView. moveToNextState()
         }

         public void onWidgetInteractionCompleted(@NotNull LiveLikeWidgetEntity widgetData) {
                      delay(10000)//10 seconds
                      widgetView. moveToNextState()
         }

         public void onWidgetDismissed(@NotNull LiveLikeWidgetEntity widgetData) {
                      delay(5)//5 seconds
                      widgetView. moveToNextState()
         }

         public void onWidgetStateChange(@NotNull WidgetStates widgetStates, @NotNull LiveLikeWidgetEntity widgetData) {
                      // we can call clearWidget() to remove current widget
                      // or keep it in finished state to build timeline mode
         }
      }));
```

## Widget Lifecycle Events

1. `onWidgetPresented(widgetData: LiveLikeWidgetEntity)` - This is called when widget is displayed on the screen or in other words when widget view is attached to its parent android view.

2. `onWidgetInteractionCompleted(widgetData: LiveLikeWidgetEntity)` - This is called when widget ineraction is completed.

3. `onWidgetDismissed(widgetData: LiveLikeWidgetEntity)` -  This is called when current displayed widget view is removed from window and destroyed.

4. `onWidgetStateChange(state: WidgetStates, widgetData: LiveLikeWidgetEntity)` - This is called when there is a widget view state change, possible states are Ready, Interacting, Results and Finished.

5. `onUserInteract(widgetData: LiveLikeWidgetEntity)` - This is called when user interact with the widget after change state to interacting.