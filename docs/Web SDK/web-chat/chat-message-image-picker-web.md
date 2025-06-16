---
title: Chat Message Image Picker (Web)
excerpt: Displaying Image Picker for sending images as chat messages
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Web Version 2.42.0+ is required

## Showing Image Picker

Chat does not show image picker by default. Add the `imagePicker`  attribute to the `livelike-chat` element to enable it.

<Embed url="https://codepen.io/abhi1599/embed/yLRxmVe" provider="codepen.io" href="https://codepen.io/abhi1599/embed/yLRxmVe" typeOfEmbed="iframe" height="300px" width="100%" iframe="true" title="undefined" />

## Customise Image Picker

Added `chatImagePickerRenderer` property to `livelike-chat` element to customise the UI for image picker window. 

The `chatImagePickerRenderer` function takes an argument object with a property called `onImageSelection`. This property is a function that expects a Blob or a URL as a string parameter. When a user selects an image, invoking `onImageSelection` with the chosen image data or location will render the image in the chat input container.

Here's an example showcasing a custom Image Picker UI and providing code snippets for rendering images in the chat input container using both Blob and URL.

<Embed url="https://codepen.io/abhi1599/embed/dyggbmy" provider="codepen.io" href="https://codepen.io/abhi1599/embed/dyggbmy" typeOfEmbed="iframe" height="300px" width="100%" iframe="true" title="undefined" />
