---
title: VOD Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
VOD (Video on demand) widgets enables you to show widgets with reference to your on demand video playback time. Every LiveLike widgets could be used as VOD widget where you just need the video playback time (in milliseconds) while creating a widget. This playback time could then be used in UI to determine which widget to be shown for a particular video moment when played by the user.

#### Get VOD widgets

You can use our existing widgets API to get VOD widgets

```javascript Javascript
LiveLike.getPostedWidgets({
  programId: "<your program Id>"
}).then((res) => {
	// In case your program has normal widget & VOD widget,
  // you can filter VOD widgets using "playback_time_ms" property
 const vodWidgets = res.widgets.filter(({playback_time_ms}) => playback_time_ms !== undefined)
})

// For large set of VOD widgets,
// you can query widgets based on since and until video playback time
LiveLike.getPostedWidgets({
  programId: "<your program Id>",
  sincePlaybackTimeMs: 200,
  untilPlaybackTimeMs: 4000 
}).then((res) => {
	// This would give you all VOD widgets that has playback time between 200 and 4000 milliseconds
  const vodWidgets = res.widgets
})
```
```kotlin Kotlin
// you can query widgets based on since and until video playback time
contentSession.getPublishedWidgets(
    GetPublishedWidgetsRequestOptions(
        liveLikePagination = page,
        sincePlaybackTimeMs = 10000,
        untilPlaybackTimeMs = 60000
    ),
    object : LiveLikeCallback<List<LiveLikeWidget>>() {
        override fun onResponse(result: List<LiveLikeWidget>?, error: String?) {
            result?.let { widgets ->
                val vodWidgets =
                    widgets // This would give you all VOD widgets that has playback time between
                            // 10000 and 60000 milliseconds
            }
        }
    }
)
```
```swift
var contentSession: ContentSession!

contentSession.getWidgetModels(
    page: .first,
    options: GetWidgetModelsRequestOptions(
        sincePlaybackMilliseconds: 10000,
        untilPlaybackMilliseconds: 60000
    ) 
) { result in
   switch result {
   case .failure(let error):
        // handle error
   case .success(let models):
        // models contains the first page of widgets with 
        // playbackTimeMilliseconds between 10000 and 60000 
   }
}
```
