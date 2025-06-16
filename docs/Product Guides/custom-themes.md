---
title: Custom Themes
excerpt: How to apply custom theming to features
deprecated: false
hidden: false
metadata:
  title: Custom Themes | LiveLike Developer Hub | Engagement SDK
  description: >-
    The Theme system allows you to customize the look of the Engagement SDK’s
    Widgets and Chat UI. Learn more about custom themes.
  robots: index
next:
  description: Link out to platform specific guides for applying themes
---
The Theme system allows you to customize the look of the Engagement SDK’s Widgets and Chat UI. This includes common UI properties such as background colors and border colors, corner radii, and text size and fonts. Those customizations are saved in a standard format and can be reused across platforms. Some common use cases for the theme system include:

* Quickly matching your application’s style with minimal development effort
* Uniquely theming Widgets for a sponsorship opportunity
* Improving the accessibility of your application or supporting alternate styles

> 📘 Minimum Supported SDK Version
>
> iOS: 2.5\
> Android: 2.1\
> Web: 1.26.3

![729](https://files.readme.io/0b181b2-b5d9ab7-6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif "b5d9ab7-6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif")

![726](https://files.readme.io/f54a914-92c017a-ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif "92c017a-ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif")

![725](https://files.readme.io/7f6f063-ba2873e-16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif "ba2873e-16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif")

## Theme System

Each widget is broken down into *components* that can be themed. Each component has a list of *component properties* that can be modified that will change the visual appearance of the component.

There are two types of components: *container components* and *text components*. Container components have other components inside of them, including text components and other container components. Each type of widget uses a base set of components, and then individual types can have more depending on the widget.

### Container Components

Container components have properties like backgrounds, borders, and corner radii. Container components usually have other container components inside them, as well as text components. The exact properties are:

* Background (Fill or Gradient)
* Border Color
* Border Width
* Corner Radii

### Text Components

Text components can have their font faces, sizes, and weights customized, as well as their colors. The exact properties are:

* Color
* Size
* Font Family
* Font Weight

## Widgets

### Alert Widgets

* Main Container
  * Header Container
    * Title Text
  * Body Container
    * Description Text (optional)
  * Footer Container (optional)
    * Link Text

### Poll, Quiz, and Prediction Widgets

* Main Container
  * Header Container
    * Title Text
  * Body Container
    * Option Container (repeated for each option)
      * Progress Bar Container
      * Option Description Text
      * Option Percentage Text

> 📘 Images in options aren't themed
>
> Polls, quizzes, and predictions have an image variant where each option also has an associated image. That image can't be themed, and always appears on the right. In the text variant, the Option Percentage takes the place of the image on the right.

### Other Widgets

> 🚧 More Widget Support Coming Soon
>
> Cheer Meters, and Rich Text can be customized using custom code, but the common theme format does not support them yet.
>
> iOS - [https://docs.livelike.com/docs/ios-custom-theming](https://docs.livelike.com/docs/ios-custom-theming)\
> Android - [https://docs.livelike.com/docs/android-customization](https://docs.livelike.com/docs/android-customization)\
> Web - [https://docs.livelike.com/docs/web-theming](https://docs.livelike.com/docs/web-theming)

## Animations

Most widgets use animations to provide user feedback. The following animations can be overridden by following the instructions on [iOS](ios-overriding-default-lottie-animations) and [Android](android-customization#section-overriding-widget-animations). Web does not have animations by default, but an example of how to add animations in Web can be [found here](web-widget-animations-tutorial).

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Widget
      </th>

      <th>
        Animations
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Poll
      </td>

      <td>
        :no_entry_sign:
      </td>
    </tr>

    <tr>
      <td>
        Image Slider
      </td>

      <td>
        :no_entry_sign:
      </td>
    </tr>

    <tr>
      <td>
        Trivia/Quiz
      </td>

      <td>
        :white_check_mark: Correct / Incorrect
      </td>
    </tr>

    <tr>
      <td>
        Prediction
      </td>

      <td>
        :white_check_mark: Stay Tuned / Correct / Incorrect
      </td>
    </tr>

    <tr>
      <td>
        Cheer Meter
      </td>

      <td>
        :white_check_mark: Win / Lose
      </td>
    </tr>

    <tr>
      <td>
        Alerts
      </td>

      <td>
        :no_entry_sign:
      </td>
    </tr>
  </tbody>
</Table>

## Chat

iOS - [https://docs.livelike.com/docs/ios-custom-theming](https://docs.livelike.com/docs/ios-custom-theming)\
Android - [https://docs.livelike.com/docs/android-customization](https://docs.livelike.com/docs/android-customization)\
Web - [https://docs.livelike.com/docs/web-theming](https://docs.livelike.com/docs/web-theming)

## Applying Theme JSON

1. Locate and load the Theme JSON in your project.
2. Use the provided SDK API to generate the objectified Theme object from the Theme JSON.
3. Apply the Theme object to SDK UI's

```swift
class SomeClass {
    // Loaded from server, local storage, text field, etc.
    // Must be compatible with `JSONSerialization.data(withJSONObject:options:)`
    let jsonObject: Any 
    
    let widgetViewController: WidgetPopupViewController
    
    func someMethod() {
        do {
            let theme = try Theme.create(fromJSONObject: jsonObject)
            widgetViewController.setTheme(theme)
        } catch {
            // Fails if json is invalid
            print(error)
        }
    }
    
}
```
```javascript
// apply theme by passing json object or theme object
LiveLike.applyTheme(livelikeThemeObject)
```
```kotlin
//Create theme object
val themeObject = LiveLikeTheme.instanceFrom(themeJsonObject)

// apply theme by passing json object or theme object
widgetView.applyTheme(liveLikeThemeObject)
widgetView.applyTheme(liveLikeThemeJsonObject)
```
