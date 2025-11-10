---
title: Native Share and Download Interface Integration (iOS, Android, React Native)
deprecated: false
hidden: false
metadata:
  robots: index
---
# Native Interface Integration

Integrate native share and download functionality for Arcade games (e.g., _Pick Your Team_) when running inside mobile webviews (iOS, Android, or React Native).
This ensures a smoother user experience for saving images or sharing content natively.

***

## Overview

When running in a native webview, Arcade games automatically detect and use native sharing or download interfaces if available.
If the native interface is **not implemented**, the system falls back to browser-based behavior.

**Priority flow:**

| Functionality | Native Detection Order                                | Fallback            |
| ------------- | ----------------------------------------------------- | ------------------- |
| **Share**     | `window.ShareInterface.share()` → `navigator.share()` | Copy to clipboard   |
| **Download**  | `window.DownloadInterface.download()`                 | HTML `<a download>` |

***

## Implementing the Native Interfaces

### Share Interface

Expose a `share` method that accepts a text string and returns a `Promise`.

```js
share(text: string): Promise<void>
```

**Parameters:**

* `text` — The message or link to share.

**Expected behavior:**

* Opens the native share dialog.
* Resolves when sharing completes.
* Rejects if the user cancels or an error occurs.

***

### Download Interface

Expose a `download` method that accepts base64 image data and saves it to device storage.

```js
download(data: string, fileName: string, mimeType: string): Promise<void>
```

**Parameters:**

* `data` — Base64-encoded image data (without prefix)
* `fileName` — Example: `"MyTeam.png"`
* `mimeType` — Example: `"image/png"`

**Expected behavior:**

* Decode the base64 string and save the image locally.
* Resolve on success; reject on error.
* Required for reliable downloads in webviews, as browser-based downloads often fail.

***

## Platform Implementations

### iOS (WKWebView)

```swift
// Add these message handlers
mWebview.configuration.userContentController.add(self, name: "share")
mWebview.configuration.userContentController.add(self, name: "download")
```

Then inject the following scripts:

```swift
window.ShareInterface = {
  share: function(text) {
    return new Promise(function(resolve, reject) {
      window._shareResolve = resolve;
      window._shareReject = reject;
      window.webkit.messageHandlers.share.postMessage({ text });
    });
  }
};
```

```swift
window.DownloadInterface = {
  download: function(data, fileName, mimeType) {
    return new Promise(function(resolve, reject) {
      const callbackId = 'dlcb_' + Math.random().toString(36).substr(2, 9);
      window.DownloadInterface._callbacks = window.DownloadInterface._callbacks || {};
      window.DownloadInterface._callbacks[callbackId] = { resolve, reject };
      window.webkit.messageHandlers.download.postMessage({ data, fileName, mimeType, callbackId });
    });
  },
  _notifySuccess(callbackId) { ... },
  _notifyFailure(callbackId, error) { ... }
};
```

**Permissions required:**

```xml
<key>NSPhotoLibraryAddUsageDescription</key>
<string>We need access to save images to your photo library</string>
```

***

### Android (WebView)

Add a `JavascriptInterface` to handle native methods:

```java
@JavascriptInterface
public void handleShare(String text) {
  runOnUiThread(() -> {
    Toast.makeText(mContext, text, Toast.LENGTH_LONG).show();
    webView.evaluateJavascript("if (window._shareResolve) window._shareResolve();", null);
  });
}
```

```java
@JavascriptInterface
public void handleDownload(String data, String fileName, String mimeType) {
  ContentResolver resolver = mContext.getContentResolver();
  ContentValues values = new ContentValues();
  values.put(MediaStore.MediaColumns.DISPLAY_NAME, fileName);
  values.put(MediaStore.MediaColumns.MIME_TYPE, mimeType);
  values.put(MediaStore.MediaColumns.RELATIVE_PATH, Environment.DIRECTORY_DOWNLOADS);
  Uri uri = resolver.insert(MediaStore.Downloads.EXTERNAL_CONTENT_URI, values);
  ...
}
```

Then inject the JS bridge:

```js
window.ShareInterface = {
  share: text => new Promise((resolve, reject) => {
    window._shareResolve = resolve;
    Android.handleShare(text);
  })
};
window.DownloadInterface = {
  download: (data, fileName, mimeType) => new Promise((resolve, reject) => {
    window._downloadResolve = resolve;
    Android.handleDownload(data, fileName, mimeType);
  })
};
```

✅ **For Android 10+**, use `MediaStore` API for saving files in `Downloads`.

***

### React Native (WebView)

```tsx
import { WebView } from 'react-native-webview'
import { Share, PermissionsAndroid } from 'react-native'
import * as FileSystem from 'expo-file-system'

const injectedJS = `
window.ShareInterface = {
  share: text => new Promise((resolve, reject) => {
    window.ReactNativeWebView.postMessage(JSON.stringify({ type: 'share', text }));
    window._shareResolve = resolve;
    window._shareReject = reject;
  })
};
window.DownloadInterface = {
  download: (data, fileName, mimeType) => new Promise((resolve, reject) => {
    window.ReactNativeWebView.postMessage(JSON.stringify({ type: 'download', data, fileName, mimeType }));
    window._downloadResolve = resolve;
    window._downloadReject = reject;
  })
};
true;
`
```

**Handle messages:**

```tsx
const handleMessage = async event => {
  const { type, data, fileName, mimeType, text } = JSON.parse(event.nativeEvent.data);

  if (type === 'share') await Share.share({ message: text });
  if (type === 'download') {
    await FileSystem.writeAsStringAsync(`${FileSystem.documentDirectory}${fileName}`, data, { encoding: FileSystem.EncodingType.Base64 });
  }
};
```

**Install dependencies:**

```bash
npm install react-native-webview expo-file-system react-native-toast-message
```

***

## Share Text Format

Games like _Pick Your Team_ send share messages in this structure:

```
[Message]\n[Image URL]\nCreate yours and share back: [Deep link URL]
```

**Example:**

```
Check out my team!
https://example.com/image.png
Create yours and share back: https://livelike.com/game/123
```

***

### ✅ Summary

| Interface                      | Purpose            | Required?   | Fallback                   |
| ------------------------------ | ------------------ | ----------- | -------------------------- |
| `ShareInterface.share()`       | Native share sheet | Optional    | `navigator.share()` / copy |
| `DownloadInterface.download()` | Native file save   | Recommended | Browser download           |

<br />
