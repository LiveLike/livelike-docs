---
title: Attaching Custom Data to Widgets
deprecated: false
hidden: false
metadata:
  robots: index
---
You can attach custom data to widgets by providing a string value in the `custom_data` field when creating a widget. All widgets support the custom data field. Since the stock user interface doesn't know how to interpret custom data, integration with [Custom Widget UI](https://docs.livelike.com/v1_doc_rewire_vk/update/docs/building-custom-widget-ui#/) would be needed to display the custom data.

The custom data field is an arbitrary string value, so data can be provided in plain text, or any encoding format that can be serialised as plain text.

> 📘 Custom data is managed via REST API
>
> Custom data can only be attached to widgets created the REST API through the `custom_data` field on each widget.

## Sample use cases

* Statistics from a sports data provider
* Links and labels for custom calls to action
* Categorisation and tagging
* Extra contextual information, like question number in a quiz game
