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
## addProgramListener

This API lets you add a listener for program based events such as widget created event whenever any widget is published. With this API you can build your own timeline of widgets.\
In case of widget created event, listener argument:

* `event` property is of type [WidgetCreated](https://livelike-doc-redirect-url.herokuapp.com/javascript?enum=WidgetCreated) enum
* `message` property is of type [IWidgetPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetPayload).

**API Definition:** [addProgramListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addProgramListener)

```javascript
import { getPostedWidgets } from '@livelike/javascript';

function programListener({ event, message }){
	// event of type WidgetCreated
  // message is of type IWidgetPayload
}

addProgramListener({
  programId: "<Your program Id>"
}, programListener)
```

## removeProgramListener

This API lets you remove a listener which was added using a `addProgramListener` API.

**API Definition:** [removeProgramListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=removeProgramListener)

```javascript
import { getPostedWidgets } from '@livelike/javascript';

function programListener({ event, message }){
	// event of type WidgetCreated
  // message is of type IWidgetPayload
}

removeProgramListener({
  programId: "<Your program Id>"
}, programListener)
```
