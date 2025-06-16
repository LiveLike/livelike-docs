---
title: Listing Widgets
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
## List Widgets For Program

Each program has a `widgets_url` hyperlink field that can be requested to get all of the widgets created that program. The widget history resource is paginated.

```python
import requests

# Fetch program resource
r = requests.get('https://cf-blast.livelikecdn.com/api/v1/programs/f1938a34-2611-4cff-9043-ad6b3dd2f6fd/')
program = r.json()

# Fetch all of a program's widgets with widgets_url
r = requests.get(program['widgets_url'])
history = r.json()
```

## Filtering Widget Lists

The default behavior is to return all widgets that have been created. The list responses can be filtered by the `status` parameter. The valid statuses are:

- `pending` List widgets that have been created but not scheduled
- `scheduled` List widgets that have been scheduled but not yet published
- `published` List widgets that have been published

### Showing Only Published Widgets

```python
# Fetch only published widgets in a program
r = requests.get(program['widgets_url'], params={'status': 'published'})
history = r.json()
```

Widgets can also be ordered by most recent.

```python
# Fetch widgets ordered by most recently published
r = requests.get(program['widgets_url'], params={'status': 'published', 'ordering': 'recent'})
recent_history = r.json()
```

### Showing Widgets Created by Specific Profile

Use the `created_by_id` query parameter to return widgets created by a given profile ID. The parameter can be specified multiple times to return widgets created by more than one profile.

```python
# Fetch published widgets authored by profile '91e9bbf9-1a51-48c6-a7fe-e0bd8cc3fc64'
requests.get(
    program["widgets_url"],
    params={
        "status": "published",
      	"created_by_id": "91e9bbf9-1a51-48c6-a7fe-e0bd8cc3fc64"
    },
)
```

<br />

### Showing Widgets of Specific Kind

Widgets can be filtered by `kind` as well.  Multiple `kind` parameters can be given.

```python
# Fetch poll widgets ordered by most recently published
r = requests.get(
    program["widgets_url"],
    params={
        "status": "published",
        "ordering": "recent",
        "kind": ["text-poll", "image-poll"],
	      "widget_attribute": "key:value",
      	"created_by_id": "91e9bbf9-1a51-48c6-a7fe-e0bd8cc3fc64"
    },
)
recent_poll_history = r.json()
```

By default the API will return 20 widgets per-page.  This limit can be increased with the `page_size` parameter.

```python
# Fetch poll widgets ordered by most recently published
r = requests.get(
    program["widgets_url"],
    params={
        "status": "published",
        "ordering": "recent",
        "kind": ["text-poll", "image-poll"],
	      "widget_attribute": "key:value",
      	"created_by_id": "91e9bbf9-1a51-48c6-a7fe-e0bd8cc3fc64"
        "page_size": 100
    },
)
recent_poll_history = r.json()
```

> 🚧 Widgets Page Size
> 
> The maximum number of widgets that can be returned in a single page is 1,000.  But be careful fetching large numbers of widgets in a single API call since rendering them on the client device can cause issues with performance and memory usage.  Using smaller page sizes and a "Load More" button can help to alleviate those issues.