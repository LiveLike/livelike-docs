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
[block:api-header]
{
  "title": "Widget View"
}
[/block]
For using the WidgetView in your flutter app, you have to add the WidgetView in your app and provide contentSession object to that widgetView.

[block:code]
{
  "codes": [
    {
      "code": "WidgetView(session: session!,\n           key: Key(session!.programId!));",
      "language": "text",
      "name": "Flutter"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "SDK Version 0.1.0-prerelease.0",
  "body": "The Below functionality is available from release version 0.1.0-prerelease.0"
}
[/block]
**WidgetListener** 
WidgetListener is used to listen to the incoming widget inside widget view

**Enable/Disable Widget Interaction Functionality**
To enable/disable the default widgetTransition 

**Change State of Widget inside WidgetView**
To change the state of the widget. 

**To Display Widget using instance of LiveLikeWidget** 
use method displayWidget inside widgetKey(GlobalKey) of WidgetView to display widget inside WidgetView
[block:code]
{
  "codes": [
    {
      "code": "final widgetKey = GlobalKey<WidgetViewState>();\n\nWidgetView(\n\t\t\t\tkey:widgetKey\n        session: session,\n        widgetListener: (widget) {\n          //LiveLikeWidget\n        },\n)\nwidgetKey.currentState?.displayWidget(<instance of LiveLikeWidget>);\nwidgetKey.currentState?.enableDefaultWidgetTransition(false);\nwidgetKey.currentState?.setWidgetState(WidgetState.Result);",
      "language": "text",
      "name": "Flutter"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Widget View with support in ListView"
}
[/block]
Now widgetView can be used with listview, you need to create an instance of widgetview and assign a key to it and then call the methods to perform the actions , below is the example of how to do this.
[block:code]
{
  "codes": [
    {
      "code": " final key = GlobalKey<WidgetViewState>();\n        final widgetView = WidgetView(\n          key: key,\n          widgetListener: (id, kind) {\n            // print(\"WidgetView>> $id >> $index\");\n          },\n          showWidgetViewWithDefaultHeight: true,\n          onWidgetViewInit: () {\n            if (key.currentState != null) {\n              await key.currentState!.enableDefaultWidgetTransition(false);\n              await key.currentState!.showDismissButton(false);\n              await key.currentState!.displayWidget(widget);\n              await Future.delayed(const Duration(seconds: 2));\n              await key.currentState!.setWidgetState(WidgetState.results);\n            }\n          },\n        );",
      "language": "text",
      "name": "Flutter"
    }
  ]
}
[/block]
after calling the display widget, if you need to change the state of the widget, make sure to do the task with some delay in time, we will be adding support for this future.

**Fetch Widget Details** 
In order to fetch details of a particular widget.
The API required widget id and widgetKind , and the result will be LiveLikeWidget model class

[block:code]
{
  "codes": [
    {
      "code": "await sdk.fetchWidgetDetails(widgetId!, widgetKind!);",
      "language": "text"
    }
  ]
}
[/block]