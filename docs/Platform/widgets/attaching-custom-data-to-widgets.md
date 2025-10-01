---
title: Attaching Custom Data to Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Attaching Custom Data to Widgets | LiveLike Developer Hub
  description: >-
    Attach custom data to widgets by providing a string value in the
    `custom_data` field when creating a widget. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: custom-widget-ui
      title: Building Custom Widget UI
---
You can attach custom data to widgets by providing a string value in the `custom_data` field when creating a widget. All widgets support the custom data field. Since the stock user interface doesn't know how to interpret custom data, integration with [Custom Widget UI](doc:custom-widget-ui) would be needed to display the custom data.

The custom data field is an arbitrary string value, so data can be provided in plain text, or any encoding format that can be serialized as plain text.

> 📘 Custom data is managed via REST API
>
> Custom data can only be attached to widgets created the REST API through the `custom_data` field on each widget.

## Sample use cases

* Statistics from a sports data provider
* Links and labels for custom calls to action
* Categorization and tagging
* Extra contextual information, like question number in a quiz game
