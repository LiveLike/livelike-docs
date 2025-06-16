---
title: Network Utils
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
## LiveLikeKotlin.request Function

TIn case you feel the need to use our backend REST API due to some extreme edge cases that our SDK API doesn't support, you can use the LiveLikeKotlin.request function which is a versatile method designed to facilitate network requests within Kotlin applications while utilizing the LiveLike platform. It offers flexibility in handling various HTTP request types (e.g., GET, POST, PUT, DELETE) and allows for customization of request parameters.

```kotlin
inline fun <B : Any, reified R : Any> LiveLikeKotlin.request(
    path: String?,
    url: String? = null,
    requestType: RequestType,
    queryParameters: List<Pair<String, Any?>> = emptyList(),
    body: B? = null,
    accessToken: String? = null,
    headers: List<Pair<String, String>> = emptyList(),
    noinline callback: LiveLikeCallback<R>
)
```

### Parameters:

* path (String?): The path for the request. Can be null if 'url' is provided.
* URL (String?): The URL for the request. Can be null if 'path' is provided.
* requestType (RequestType): The type of HTTP request (e.g., GET, POST, PUT, DELETE).
* queryParameters (List<Pair<String, Any?>>): The query parameters for the request as a list of key-value pairs.
* body (B?): The request body, if applicable.
* accessToken (String?): The access token for authorization. Can be null if not required.
* headers (List<Pair<String, String>>): Additional headers for the request as a list of key-value pairs.
* callback (LiveLikeCallback<R>): The callback to handle the asynchronous response.

## How to Use

To utilize this function:

Import the necessary classes/interfaces required for LiveLikeKotlin and LiveLikeCallback.\
Call the request function with appropriate parameters based on your request needs.\
Implement the callback to handle the response once it's received.

```kotlin
// Example usage of LiveLikeKotlin.request function

val path = "/example/path"
val requestType = RequestType.GET
val queryParameters = listOf("param1" to "value1", "param2" to 123)
val accessToken = "your_access_token"

LiveLikeKotlin.request<String, YourResponseClass>(
    path = path,
    requestType = requestType,
    queryParameters = queryParameters,
    accessToken = accessToken,
    callback = { response:YourResponseClass?, error:String? -> 
    
    }
)
```

Replace **YourResponseClass** with the actual response data class you expect from the server.