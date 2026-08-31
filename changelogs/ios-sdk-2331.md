---
title: iOS SDK 2.33.1
author: jelzon monzon
hidden: false
published_at: '2021-10-13T20:05:55.083Z'
---
## Bug Fixes

* Added theme options for the Stock UI of the Quiz Widget. Add the `submitButtonEnabled` and `submitButtonDisabled` components to your theme json. See sample below.

```json
{
  "version": 1,
  "widgets": {
    "quiz": {
      "submitButtonEnabled": {
        "borderRadius": [
          0,
          0,
          0,
          0
        ],
        "padding": [
          0,
          0,
          0,
          0
        ],
        "fontFamily": [
          "sans-serif"
        ],
        "fontSize": 16,
        "borderWidth": 0,
        "fontWeight": "normal",
        "margin": [
          0,
          0,
          0,
          0
        ],
        "borderColor": "00000000",
        "fontColor": "ffffff",
        "background": {
          "color": "00000000",
          "format": "fill"
        }
      },
      "submitButtonDisabled": {
        "borderRadius": [
          0,
          0,
          0,
          0
        ],
        "padding": [
          0,
          0,
          0,
          0
        ],
        "fontFamily": [
          "sans-serif"
        ],
        "fontSize": 16,
        "borderWidth": 0,
        "fontWeight": "normal",
        "margin": [
          0,
          0,
          0,
          0
        ],
        "borderColor": "00000000",
        "fontColor": "ffffff",
        "background": {
          "color": "00000000",
          "format": "fill"
        }
      }
    }
  }
}
```