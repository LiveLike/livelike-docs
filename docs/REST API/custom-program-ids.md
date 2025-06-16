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
## Set a Custom ID on a program

Programs can have Custom IDs set on them when creating or editing events inside the CMS.

![579](https://files.readme.io/0773e1e-image001.png "image001.png")

> 🚧 Ensure the Custom ID is unique
>
> No two programs may have the same custom ID.

## Look up program by Custom ID

Use the `program_custom_id_url_template` value on your application resource to build a URL to send a request to. Here is a simplified sample app resource for client ID `example-client-id` showing that field:

```json app.json
{
  "id": "example-client-id",
  "url": "https://cf-blast.livelikecdn.com/api/v1/applications/example-client-id/",
  "program_custom_id_url_template": "https://cf-blast.livelikecdn.com/api/v1/program-by-custom-id/example-client-id/{custom_id}/"
}
```

Using that field, and a Custom ID of `example-custom-id`, the URL to a program using a Custom ID would look like:

```
https://cf-blast.livelikecdn.com/api/v1/program-by-custom-id/example-client-id/example-custom-id/
```
