---
title: Chat Message Image Picker (Android)
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
The stock chat interface on Android provides an image picker.

# Custom Image Picker

This has been added to chat UI and also there is option to render custom UI.

```kotlin
binding.chatWidget.chatView.chatImagePickerDelegate =
    object : ChatImagePickerDelegate {
        override fun onImageButtonClicked() {
          // this opens up the dialog, to navigate to gallery
          // Custom UI can also be rendered for this
            openPickerDialog()
        }
    
        // opens up the dialog to navigate to gallery
        private fun openPickerDialog() {
            // Give your custom view for image picker dialog here
            // Here AlertDialog is used as an example
          
        val builder = AlertDialog.Builder(context)
        builder.setView(R.layout.bottom_sheet_layout)
        val dialog = builder.create()
        dialog.window?.decorView?.setBackgroundResource(R.drawable.dialog_background) // setting the background
        dialog.show()
        dialog.findViewById<TextView>(R.id.photo_tv)?.setOnClickListener {
            dialog.dismiss()
            pickMedia.launch(PickVisualMediaRequest(ActivityResultContracts.PickVisualMedia.ImageOnly))
       }
         }
    }
```