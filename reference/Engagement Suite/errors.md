---
title: Errors
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
The API tries to return as descriptive an error message as possible along with a meaningful status code. Response status codes in the 400 range indicate a client error and must be addressed by the client before retrying. Status codes in the 500 range indicate an internal LiveLike error and can be retried without modifying the request. These response codes include:

* 400 Bad Request. The request was malformed in some way, oftentimes caused by a missing or invalid field.
* 401 Unauthorized. The request was made without authorization to a resource that requires it.
* 403 Forbidden. The request was made with authorization, but is not permitted to access the resource.
* 404 Not Found. The request was made to a resource that does not exist.
* 409 Conflict. The request was made but conflicts with a previously issued request.
* 500 Internal Server Error. The request was made but the server experienced a transient issue while handling it.
