---
title: Customizing Widgets UI
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The `Theme` class can be used to override default values set to generate the stock UI for `Widgets` to customise or modify the UI to match your needs.  Listed below are the options to customise the different types of `Widgets` using the attributes in `Theme`

Users can customise the Stock UI Version when initialising the `Theme` class. It accepts a parameter for `stockUIVersion` which can be either `.v1` or `.v2`

## Alert Widget

The `Alert Widgets` are created as a stack of three different views which are `Header` , `Body` and `Footer`.

The `Main`, `Header`, `Body` and `Footer` sections of the widget are of type `Theme.Container`  
To customise the UI for the `Alert Widget` as a whole you can edit the values for the attributes in `main`

```swift
let theme = Theme()
theme.widgets.alert.main = Theme.Container(
  background: .fill(color: UIColor(red: 0.07, green: 0.08, blue: 0.14, alpha: 1)),
  borderColor: .clear,
  borderWidth: 0,
  cornerRadii: CornerRadii(all: widgetV2CornerRadius),
 	topMargin: 0,
  bottomMargin: 0,
  leadingMargin: 0,
  trailingMargin: 0,
  contentSpacing: 0
)
widgetViewController.setTheme(theme)
```

The individual values for the same can also be updated as shown below:

```swift
let theme = Theme()
theme.widgets.alert.main.borderColor = .red
widgetViewController.setTheme(theme)
```

The `title` which is a part of the `Header` and the `description` which is a part of the `Body` of the `Alert Widget` can be customised by changing the attributes in the `Theme.Label`

```
let theme = Theme()
theme.widgets.alert.title = Theme.Label(
  color: widgetTextColor,
  font: widgetTitleFont,
  topPadding: 16,
  leadingPadding: 16,
  trailingPadding: -16,
  bottomPadding: -4
)
widgetViewController.setTheme(theme)
```

```
let theme = Theme()
theme.widgets.alert.main.borderColor = .red
widgetViewController.setTheme(theme)
```

### Text and Image Alert Widget

The spacing between Text and Image in this particular kind of Widget can be customised using the `contentSpacing` attribute of the `Container` object in `Theme`

### Alert Widget with Link

The look of the `link` in the `Footer` of the `Alert Widget` can be customised by editing the attributes for `theme.widgets.alert.link` as a `Theme.Text` object

## Poll Widget

The `Poll Widgets` are created as a stack of three different views which are `Header` , `Body` and `Footer`.

The `Main`, `Header`, `Body` and `Footer` sections of the widget are of type `Theme.Container`  
To customise the UI for the `Poll Widget` as a whole you can edit the values for the attributes in as mentioned above for the `Alert Widget`.

For `Poll Widgets`, users have additional options to customise the `Choice Options` in a `Poll Widget`. The following attributes are available to change. Users can change options for `unselectedOption` or `selectedOption`.

```swift
let unselectedOption = Theme.ChoiceWidget.Option(
	container: Container(
  	background: .fill(color: .black),
    borderColor: .clear,
    borderWidth: 2,
    cornerRadii: CornerRadii(all: widgetOptionCornerRadius),
    topMargin: 0,
    bottomMargin: 0,
    leadingMargin: 0,
    trailingMargin: 0,
    contentSpacing: 0
	),
  description: Text(
    color: widgetTextColor,
    font: widgetOptionTextFont
  ),
    percentage: Text(
      color: widgetTextColor,
      font: UIFont.preferredFont(forTextStyle: .headline).livelike_bold()
	),
  progressBar: ProgressBar(
    background: .fill(color: .clear),
    borderColor: .clear,
    borderWidth: 0,
    cornerRadii: CornerRadii(all: 3),
      height: 28
		),
    topPadding: 0,
    leadingPadding: 0,
    trailingPadding: 0,
    bottomPadding: 0
)
```

Users can also update singular attributes and values by using code snippets as the following:

```swift
let theme = Theme()
theme.widgets.poll.unselectedOption.progressBar.backgroundColor = .red
widgetViewController.setTheme(theme)
```