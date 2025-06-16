---
title: Program
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
[block:api-header]
{
  "title": "addProgramListener"
}
[/block]
This API lets you add a listener for program based events such as widget created event whenever any widget is published. With this API you can build your own timeline of widgets.
In case of widget created event, listener argument:
* `event` property is of type [WidgetCreated](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=WidgetCreated) enum
* `message` property is of type [IWidgetPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetPayload).

**API Definition:** [addProgramListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addProgramListener)
[block:code]
{
  "codes": [
    {
      "code": "import { getPostedWidgets } from '@livelike/javascript';\n\nfunction programListener({ event, message }){\n\t// event of type WidgetCreated\n  // message is of type IWidgetPayload\n}\n\naddProgramListener({\n  programId: \"<Your program Id>\"\n}, programListener)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "removeProgramListener"
}
[/block]
This API lets you remove a listener which was added using a `addProgramListener` API.

**API Definition:** [removeProgramListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=removeProgramListener)
[block:code]
{
  "codes": [
    {
      "code": "import { getPostedWidgets } from '@livelike/javascript';\n\nfunction programListener({ event, message }){\n\t// event of type WidgetCreated\n  // message is of type IWidgetPayload\n}\n\nremoveProgramListener({\n  programId: \"<Your program Id>\"\n}, programListener)",
      "language": "javascript"
    }
  ]
}
[/block]