---
title: Widget View
excerpt: Showing LiveLike WidgetView in your flutter App
deprecated: false
hidden: false
metadata:
  title: Widget View | Flutter SDK | LiveLike Developer Hub
  description: >-
    To use the WidgetView in your Flutter app, add the WidgetView in your app
    and provide contentSession object to that widgetView.
  robots: index
next:
  description: ''
---
## Widget View

For using the WidgetView in your flutter app, you have to add the WidgetView in your app and provide contentSession object to that widgetView.

```text Flutter
WidgetView(session: session!,
           key: Key(session!.programId!));
```

> 🚧 SDK Version 0.1.0-prerelease.0
>
> The Below functionality is available from release version 0.1.0-prerelease.0

**WidgetListener**\
WidgetListener is used to listen to the incoming widget inside widget view

**Enable/Disable Widget Interaction Functionality**\
To enable/disable the default widgetTransition 

**Change State of Widget inside WidgetView**\
To change the state of the widget. 

**To Display Widget using instance of LiveLikeWidget**\
use method displayWidget inside widgetKey(GlobalKey) of WidgetView to display widget inside WidgetView

```text Flutter
final widgetKey = GlobalKey<WidgetViewState>();

WidgetView(
				key:widgetKey
        session: session,
        widgetListener: (widget) {
          //LiveLikeWidget
        },
)
widgetKey.currentState?.displayWidget(<instance of LiveLikeWidget>);
widgetKey.currentState?.enableDefaultWidgetTransition(false);
widgetKey.currentState?.setWidgetState(WidgetState.Result);
```

## Widget View with support in ListView

Now widgetView can be used with listview, you need to create an instance of widgetview and assign a key to it and then call the methods to perform the actions , below is the example of how to do this.

```text Flutter
final key = GlobalKey<WidgetViewState>();
        final widgetView = WidgetView(
          key: key,
          widgetListener: (id, kind) {
            // print("WidgetView>> $id >> $index");
          },
          showWidgetViewWithDefaultHeight: true,
          onWidgetViewInit: () {
            if (key.currentState != null) {
              await key.currentState!.enableDefaultWidgetTransition(false);
              await key.currentState!.showDismissButton(false);
              await key.currentState!.displayWidget(widget);
              await Future.delayed(const Duration(seconds: 2));
              await key.currentState!.setWidgetState(WidgetState.results);
            }
          },
        );
```

after calling the display widget, if you need to change the state of the widget, make sure to do the task with some delay in time, we will be adding support for this future.

**Fetch Widget Details**\
In order to fetch details of a particular widget.\
The API required widget id and widgetKind , and the result will be LiveLikeWidget model class

```text
await sdk.fetchWidgetDetails(widgetId!, widgetKind!);
```
