---
title: Widget Configuration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Configuration | Android SDK | LiveLike
  description: >-
    Learn how to intercept widgets with our Android SDK Widget Configuration
    information guide.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Intercept Widgets"
}
[/block]
Widgets can be **intercepted** to add a Toast before showing the widget or delaying them until the user approve to see them.

1. Create a WidgetInterceptor

2. widgetWantsToShow() will be called by the SDK when a widget is ready to be shown on screen.

3. At this time Call `ShowWidget()` to show the widget or `dismissWidget()` to dismiss it.

[block:code]
{
  "codes": [
    {
      "code": "// Example of Widget Interceptor showing a dialog\n    private val interceptor = object : WidgetInterceptor() {\n            override fun widgetWantsToShow() {\n                AlertDialog.Builder(context).apply {\n                    setMessage(\"You received a Widget, what do you want to do?\")\n                    setPositiveButton(\"Show\") { _, _ ->\n                        showWidget() // Releases the widget\n                    }\n                    setNegativeButton(\"Dismiss\") { _, _ ->\n                        dismissWidget() // Discards the widget\n                    }\n                    create()\n                }.show()\n            }\n        }\n    \n    // You just need to add it on your session instance\n    session.widgetInterceptor = interceptor",
      "language": "text",
      "name": "Kotlin"
    },
    {
      "code": "// Example of Widget Interceptor showing a dialog\nWidgetInterceptor interceptor =  new WidgetInterceptor() {\n             @Override\n             public void widgetWantsToShow(@NotNull LiveLikeWidgetEntity widgetData) {\n                 new AlertDialog.Builder(context)\n                     .setMessage(\"You received a Widget, what do you want to do?\")\n                     .setPositiveButton(\"Show\", new DialogInterface.OnClickListener() {\n                                 @Override\n                                 public void onClick(DialogInterface dialog, int which) {\n                                     showWidget(); // Releases the widget                                     \n                                 }\n                             })\n                     .setNegativeButton(\"Dismiss\", new DialogInterface.OnClickListener() {\n                         @Override\n                         public void onClick(DialogInterface dialog, int which) {\n                             dismissWidget(); // Discards the widget\n                         }\n                     })\n                     .create()\n                    .show();\n             }\n         };\n\n// You just need to add it on your session instance\nsession.setWidgetInterceptor(interceptor);",
      "language": "text",
      "name": "Java"
    }
  ]
}
[/block]