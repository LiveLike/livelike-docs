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
## Intercept Widgets

Widgets can be **intercepted** to add a Toast before showing the widget or delaying them until the user approve to see them.

1. Create a WidgetInterceptor

2. widgetWantsToShow() will be called by the SDK when a widget is ready to be shown on screen.

3. At this time Call `ShowWidget()` to show the widget or `dismissWidget()` to dismiss it.

```text Kotlin
// Example of Widget Interceptor showing a dialog
    private val interceptor = object : WidgetInterceptor() {
            override fun widgetWantsToShow() {
                AlertDialog.Builder(context).apply {
                    setMessage("You received a Widget, what do you want to do?")
                    setPositiveButton("Show") { _, _ ->
                        showWidget() // Releases the widget
                    }
                    setNegativeButton("Dismiss") { _, _ ->
                        dismissWidget() // Discards the widget
                    }
                    create()
                }.show()
            }
        }
    
    // You just need to add it on your session instance
    session.widgetInterceptor = interceptor
```
```text Java
// Example of Widget Interceptor showing a dialog
WidgetInterceptor interceptor =  new WidgetInterceptor() {
             @Override
             public void widgetWantsToShow(@NotNull LiveLikeWidgetEntity widgetData) {
                 new AlertDialog.Builder(context)
                     .setMessage("You received a Widget, what do you want to do?")
                     .setPositiveButton("Show", new DialogInterface.OnClickListener() {
                                 @Override
                                 public void onClick(DialogInterface dialog, int which) {
                                     showWidget(); // Releases the widget                                     
                                 }
                             })
                     .setNegativeButton("Dismiss", new DialogInterface.OnClickListener() {
                         @Override
                         public void onClick(DialogInterface dialog, int which) {
                             dismissWidget(); // Discards the widget
                         }
                     })
                     .create()
                    .show();
             }
         };

// You just need to add it on your session instance
session.setWidgetInterceptor(interceptor);
```
