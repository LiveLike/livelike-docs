---
title: Custom Program IDs
excerpt: How to use Custom IDs with programs
deprecated: false
hidden: false
metadata:
  title: Custom Program IDs | REST API | LiveLike Developer Hub
  description: >-
    Programs can have Custom IDs set on them when creating or editing events
    inside the CMS. Learn how to use Custom IDs with programs.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Set a Custom ID on a program"
}
[/block]
Programs can have Custom IDs set on them when creating or editing events inside the CMS.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0773e1e-image001.png",
        "image001.png",
        579,
        606,
        "#2d313d"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Ensure the Custom ID is unique",
  "body": "No two programs may have the same custom ID."
}
[/block]

[block:api-header]
{
  "title": "Look up program by Custom ID"
}
[/block]
Use the `program_custom_id_url_template` value on your application resource to build a URL to send a request to. Here is a simplified sample app resource for client ID `example-client-id` showing that field:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"id\": \"example-client-id\",\n  \"url\": \"https://cf-blast.livelikecdn.com/api/v1/applications/example-client-id/\",\n  \"program_custom_id_url_template\": \"https://cf-blast.livelikecdn.com/api/v1/program-by-custom-id/example-client-id/{custom_id}/\"\n}",
      "language": "json",
      "name": "app.json"
    }
  ]
}
[/block]
Using that field, and a Custom ID of `example-custom-id`, the URL to a program using a Custom ID would look like:

```
https://cf-blast.livelikecdn.com/api/v1/program-by-custom-id/example-client-id/example-custom-id/
```