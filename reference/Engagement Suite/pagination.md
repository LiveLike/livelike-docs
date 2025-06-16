---
title: Pagination
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
Collection resources are paginated in the API. All paginated resources are returned wrapped in an envelope with `count`,  `next`, `previous`, and `results` fields:

```json
{
  "count": 100, /* the total number of items across all pages */
  "next": "https://example.com/api/v1/resources/?page=3",
  "previous": "https://example.com/api/v1/resources/?page=1",
  "results": [
    /* items on page 2 of this collection */
  ]
}
```

The `results` field contains the items in that page. If the `next` field is non-null then the next page is available. If the `previous` field is non-null then the previous page is available.
