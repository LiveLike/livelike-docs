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
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"count\": 100, /* the total number of items across all pages */\n  \"next\": \"https://example.com/api/v1/resources/?page=3\",\n  \"previous\": \"https://example.com/api/v1/resources/?page=1\",\n  \"results\": [\n    /* items on page 2 of this collection */\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
The `results` field contains the items in that page. If the `next` field is non-null then the next page is available. If the `previous` field is non-null then the previous page is available.