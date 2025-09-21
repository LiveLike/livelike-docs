---
title: Delete Widgets
excerpt: Deleting widgets
deprecated: false
hidden: false
metadata:
  robots: index
---
| Property    | Description                    | Required |
| :---------- | :----------------------------- | :------- |
| Widget ID   | The id of the widget to delete | Yes      |
| Widget Kind | The kind of widget to delete   | Yes      |

<details>
  <summary>Delete Widget</summary>

  ```javascript Web
  LiveLike.deleteWidget({
    widgetId: '<widget-id>',
    widgetKind: '<widget-kind>',
  }).then((res) => console.log(res));

  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.deleteWidget(
    options: DeleteWidgetRequestOptions(
      kind: <widget-kind>,
      id: "<widget-id>"
    )
  ) { result
  	switch result {
    case .success(let widget):
      break
    case .failure(let error):
      break
    }
  }
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.deleteWidget(
          request = DeleteWidgetRequest(
                 type = liveLikeWidget.getWidgetType()!!,
                 id = liveLikeWidget.id),
    			{ result, error -> })
  ```
</details>
