---
title: Native Interface Integration (iOS, Android, React Native)
excerpt: >-
  This document explains how to integrate native share and download
  functionality for the Arcade games when running in a webview (iOS/Android).
deprecated: false
hidden: true
metadata:
  robots: index
---
#

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
        // Inject the ShareInterface script
        let shareScript = """
        window.ShareInterface = {
            share: function(text) {
                return new Promise(function(resolve, reject) {
                    window._shareResolve = resolve;
                    window._shareReject = reject;
                    window.webkit.messageHandlers.share.postMessage({ text: text });
                });
            }
        };
        """
        let shareUserScript = WKUserScript(source: shareScript,
                                      injectionTime: .atDocumentEnd,
                                           forMainFrameOnly: false)


        // Inject the DownloadInterface script
        let downloadScript = """
        window.DownloadInterface = {
            download: function(data, fileName, mimeType) {
                return new Promise(function(resolve, reject) {
                    var callbackId = 'dlcb_' + Math.random().toString(36).substr(2, 9);
                    window.DownloadInterface._callbacks = window.DownloadInterface._callbacks || {};
                    window.DownloadInterface._callbacks[callbackId] = {resolve: resolve, reject: reject};
                    window.webkit.messageHandlers.download.postMessage({
                        data: data,
                        fileName: fileName,
                        mimeType: mimeType,
                        callbackId: callbackId
                    });
                });
            },
            _notifySuccess: function(callbackId) {
                var cb = window.DownloadInterface._callbacks && window.DownloadInterface._callbacks[callbackId];
                if (cb && cb.resolve) cb.resolve();
                if (window.DownloadInterface._callbacks) delete window.DownloadInterface._callbacks[callbackId];
            },
            _notifyFailure: function(callbackId, error) {
                var cb = window.DownloadInterface._callbacks && window.DownloadInterface._callbacks[callbackId];
                if (cb && cb.reject) cb.reject(new Error(error || "Download failed"));
                if (window.DownloadInterface._callbacks) delete window.DownloadInterface._callbacks[callbackId];
            }
        };
        """
        let downloadUserScript = WKUserScript(source: downloadScript,
                                              injectionTime: .atDocumentEnd,
                                              forMainFrameOnly: false)

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
    webView.evaluateJavascript("if (window._shareResolve) { window._shareResolve(); delete window._shareResolve; delete window._shareReject; }", null);
            });
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
  Uri imageUri = resolver.insert(MediaStore.Downloads.EXTERNAL_CONTENT_URI, contentValues);
                if (imageUri == null) {
                    throw new IOException("Failed to create new MediaStore record.");
                }

                try (final OutputStream os = resolver.openOutputStream(imageUri)) {
                    byte[] decodedString = Base64.decode(data, Base64.DEFAULT);
                    os.write(decodedString);
                }

                runOnUiThread(() -> {
                    Toast.makeText(mContext, fileName + " saved to Downloads", Toast.LENGTH_LONG).show();
                    webView.evaluateJavascript("if (window._downloadResolve) { window._downloadResolve(); delete window._downloadResolve; delete window._downloadReject; }", null);
                });

}
```

Then inject the JS bridge:

```java
 webView.setWebViewClient(new WebViewClient() {
            @Override
            public void onPageFinished(WebView view, String url) {
                super.onPageFinished(view, url);
                String jsWrapper = "(function() {" +
                  "window.ShareInterface = {" +
                  "  share: function(text) {" +
                  "    return new Promise(function(resolve, reject) {" +
                  "      window._shareResolve = resolve;" +
                  "      window._shareReject = reject;" +
                  "      Android.handleShare(text);" +
                  "    });" +
                  "  }" +
                  "};" +
                  "window.DownloadInterface = {" +
                  "  download: function(data, fileName, mimeType) {" +
                  "    return new Promise(function(resolve, reject) {" +
                  "      window._downloadResolve = resolve;" +
                  "      window._downloadReject = reject;" +
                  "      Android.handleDownload(data, fileName, mimeType);" +
                  "    });" +
                  "  }" +
                  "};" +
                "})()";
                view.evaluateJavascript(jsWrapper, null);
            }
        });
```

✅ **For Android 10+**, use `MediaStore` API for saving files in `Downloads`.

***

### React Native (WebView)

```typescript GameWebView.tsx
import * as FileSystem from "expo-file-system/legacy";
import React, { useRef } from "react";
import { PermissionsAndroid, Platform, Share, StyleSheet } from "react-native";
import Toast from "react-native-toast-message";
import { WebView } from "react-native-webview";

interface GameWebViewProps {
  url: string;
}

export const GameWebView: React.FC<GameWebViewProps> = ({ url }) => {
  const webViewRef = useRef<WebView>(null);

  // inject JavaScript to expose both share and download interfaces
  const injectedJavaScript = `
    window.ShareInterface = {
      share: function(text) {
        return new Promise(function(resolve, reject) {
          window.ReactNativeWebView.postMessage(JSON.stringify({
            type: 'share',
            text: text
          }));
          // store callbacks
          window._shareResolve = resolve;
          window._shareReject = reject;
        });
      }
    };
    window.DownloadInterface = {
      download: function(data, fileName, mimeType) {
        return new Promise(function(resolve, reject) {
          window.ReactNativeWebView.postMessage(JSON.stringify({
            type: 'download',
            data: data,
            fileName: fileName,
            mimeType: mimeType
          }));
          window._downloadResolve = resolve;
          window._downloadReject = reject;
        });
      }
    };
    true; // note: this is required, or you'll sometimes get silent failures
  `;

  const handleDownload = async (
    base64Data: string,
    fileName: string,
    mimeType: string
  ) => {
    try {
      // request storage permission on Android
      if (Platform.OS === "android") {
        const granted = await PermissionsAndroid.request(
          PermissionsAndroid.PERMISSIONS.WRITE_EXTERNAL_STORAGE
        );
        if (granted !== PermissionsAndroid.RESULTS.GRANTED) {
          webViewRef.current?.injectJavaScript(`
            if(window._downloadReject) window._downloadReject(new Error('Permission denied'));
            true;
          `);
          return;
        }
      }

      // save file to app's document directory (private to the app)
      // iOS: Documents directory in app sandbox
      // Android: App data directory
      const downloadsPath = FileSystem.documentDirectory;
      if (!downloadsPath) {
        throw new Error("Could not access document directory");
      }

      const filePath = `${downloadsPath}${fileName}`;

      // write base64 data to file
      await FileSystem.writeAsStringAsync(filePath, base64Data, {
        encoding: FileSystem.EncodingType.Base64,
      });

      // show success toast
      Toast.show({
        type: "success",
        text1: "Downloaded successfully",
        text2: `${fileName} saved to app storage`,
      });

      // resolve promise
      webViewRef.current?.injectJavaScript(`
        if(window._downloadResolve) window._downloadResolve();
        true;
      `);
    } catch (error: any) {
      webViewRef.current?.injectJavaScript(`
        if(window._downloadReject) window._downloadReject(new Error('${error.message.replace(
          /'/g,
          "\\'"
        )}'));
        true;
      `);
    }
  };

  return (
    <WebView
      ref={webViewRef}
      source={{ uri: url }}
      injectedJavaScript={injectedJavaScript}
      onMessage={handleMessage}
      javaScriptEnabled={true}
      domStorageEnabled={true}
      style={styles.webview}
    />
  );
};

const styles = StyleSheet.create({
  webview: {
    flex: 1,
  },
});

```

**Handle messages:**

```typescript code.tsx
const handleMessage = async (event: any) => {
    try {
      const data = JSON.parse(event.nativeEvent.data);

      if (data.type === "download") {
        await handleDownload(data.data, data.fileName, data.mimeType);
      } else if (data.type === "share") {
        Share.share({
          message: data.text,
        })
          .then((result) => {
            if (result.action === Share.sharedAction) {
              // share was successful
              Toast.show({
                type: "success",
                text1: "Shared successfully",
                text2: "Your content has been shared",
              });
              webViewRef.current?.injectJavaScript(`
                if(window._shareResolve) window._shareResolve();
                true;
              `);
            } else if (result.action === Share.dismissedAction) {
              // share was dismissed
              webViewRef.current?.injectJavaScript(`
                if(window._shareReject) window._shareReject(new Error('User cancelled'));
                true;
              `);
            }
          })
          .catch((error) => {
            webViewRef.current?.injectJavaScript(`
              if(window._shareReject) window._shareReject(new Error('${error.message.replace(
                /'/g,
                "\\'"
              )}'));
              true;
            `);
          });
      }
    } catch (error) {
      console.error("Error handling message:", error);
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