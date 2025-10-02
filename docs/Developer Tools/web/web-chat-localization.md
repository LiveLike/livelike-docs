---
title: Web Localization
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Localization | Web SDK | LiveLike Developer Hub
  description: >-
    As an integrator you have the ability to localize the Web Engagement SDK
    chat and widget experience. Learn more.
  robots: index
next:
  description: ''
---
As an integrator you have the ability to localize the EngagementSDK features. Multiple languages can be used, and they can be changed on the fly.

The built-in user interface provided by the web SDK is internationalized so that things like placeholder text, button labels, and other UI elements can be localized as part of the integration. Localizations are provided in the _localization object_ format, and localizations can be added at init or at runtime. The HTML elements provided by the LiveLike SDK respect the `lang` attribute and will use the corresponding localization key if it exists.

## The localization object

Localizations are represented as nested objects. The outer object keys are [ISO 639-1 Language Codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes), and the inner objects are mappings from placeholder keys to their localized values.

The SDK comes with an English localization by default, with this structure:

```javascript Default localization
"en": {
  "chat.inputPlaceholder": "Say something...",
  "chat.messageMenu.blockUser": "Block this user",
  "chat.messageMenu.reportMessage": "Report message",
  "chat.messageMenu.cancel": "Cancel",
  "chat.messageMenu.ariaLabel": "Message options",
  "chat.blockConfirmation.message": "You will no longer see messages from this user.",
  "chat.reportConfirmation.message": "The message has been reported to the moderators. Thank you.",
  "chat.mutedMessage": "Unable to send message.",
  "chat.errorMessage": "There was an error. Please try again.",
  "chat.messageDeleted": "This message has been removed.",
  "chat.sendButton.ariaLabel": "Send Message",
  "chat.scrollDownButton.ariaLabel": "Scroll Down",
  "chat.stickerPicker.title": "STICKERS",
  "chat.stickerPicker.openButton.ariaLabel": "Open Stickers",
  "chat.stickerPicker.closeButton.ariaLabel": "Close Stickers",
  "chat.stickerPicker.stickerPackTab.ariaLabel": "Sticker pack <packName>",
  "chat.stickerPicker.stickerSelectionButton.ariaLabel": "<stickerName> Sticker",
  "chat.giphyPicker.title": "GIPHY",
  "chat.giphyPicker.placeholder": "Search GIFs via GIPHY",
  "chat.giphyPicker.openButton.ariaLabel": "Open GIPHY",
  "chat.giphyPicker.closeButton.ariaLabel": "Close GIPHY",
  "chat.giphyPicker.stickerSelectionButton.ariaLabel": "<stickerName> GIF",
  "chat.reactions.openButton.ariaLabel": "Message reactions",
  "chat.reactions.reactionSelectionButton.ariaLabel": "Reaction <reactionName>",
  "widget.quiz.voteButton.label": "Vote",
  "widget.quiz.votedText": "Voted!",
  "widget.slider.voteButton.label": "Vote",
  "widget.slider.votedText": "Voted!",
  "widget.textAsk.placeholder": "Type something...",
  "widget.textAsk.sendButton.label": "SEND",
  "widget.video.playbackError": "Can’t play this video",
  "widget.sponsors.label": "Sponsored by",
  "widget.quiz.tag": "",
  "widget.poll.tag": "",
  "widget.prediction.tag": "",
  "widget.followup.tag": "",
}
```

<br />

## Setting the UI language

Set the `lang` attribute on elements provided by the LiveLike SDK to set the language for that tag. The `lang` attribute value should be one of the language codes supplied by a localization object.

For example, if a Spanish localization is used, the language code is `es`. The `es` language code will be used as both the `localizedStrings` key, and the `lang` attribute.

```html
<livelike-chat lang="es" roomid=""></livelike-chat>
<script>
LiveLike.init({
  clientId: '',
  localizedStrings: {
    es: {
      "chat.inputPlaceholder": "Dices Algo",
      "chat.messageMenu.blockUser": "Bloquea a esta persona",
      "chat.messageMenu.reportMessage": "Reporte este mensaje",
      "chat.messageMenu.cancel": "Cancelar",
      "chat.messageMenu.ariaLabel": "Opciones de mensaje",
      "chat.blockConfirmation.message": "Ya no recibirás mensajes de <username>.",
      "chat.reportConfirmation.message": "El mensaje ha sido informado a los moderadores. Gracias.",
      "chat.errorMessage": "Hubo un error. Inténtalo de nuevo.",
      "chat.messageDeleted": "Este mensaje ha sido eliminado.",
      "chat.sendButton.ariaLabel": "Enviar mensaje",
      "chat.scrollDownButton.ariaLabel": "Desplazarse hacia abajo",
      "chat.stickerPicker.title": "Pegatinas",
      "chat.stickerPicker.openButton.ariaLabel": "Abrir pegatinas",
      "chat.stickerPicker.closeButton.ariaLabel": "Cerrar pegatinas",
      "chat.stickerPicker.stickerPackTab.ariaLabel": "Paquete de pegatinas <packName>",
      "chat.stickerPicker.stickerSelectionButton.ariaLabel": "<stickerName> pegatina",
      "chat.giphyPicker.title": "GIPHY",
      "chat.giphyPicker.placeholder": "Buscar GIF a través de GIPHY",
      "chat.giphyPicker.openButton.ariaLabel": "Abrir GIPHY",
      "chat.giphyPicker.closeButton.ariaLabel": "Cerrar GIPHY",
      "chat.giphyPicker.stickerSelectionButton.ariaLabel": "<stickerName> GIF",
      "chat.reactions.openButton.ariaLabel": "Reacciones de mensajes",
      "chat.reactions.reactionSelectionButton.ariaLabel": "Reacción <reactionName>"
    }
  }       
})
</script>
```

<br />

## Adding UI localizations

Add localizations by passing a localization object to `LiveLike.init` method's `localizedStrings` argument, or the `LiveLike.applyLocalization` method.

### Add a UI localization at runtime

Localizations can be added at runtime by passing a localization object to the `LiveLike.applyLocalization` method.

```javascript
LiveLike.applyLocalization({
  hi: {
    "chat.inputPlaceholder": "कुछ बोलो...",
    "chat.messageMenu.blockUser": "इस उपयोगकर्ता को ब्लॉक करें",
    "chat.messageMenu.reportMessage": "रिपोर्ट संदेश",
    "chat.messageMenu.cancel": "रद्द करें",
    "chat.blockConfirmation.message": "अब आप <username> के संदेश नहीं देखेंगे",
    "chat.reportConfirmation.message": "यह संदेश मध्यस्थों को सूचित किया गया है। धन्यवाद।",
    "chat.errorMessage": "एक त्रुटि हुई। कृपया पुन: प्रयास करें।",
    "chat.messageDeleted": "यह संदेश हटा दिया गया है।",
    "chat.stickerPicker.title": "STICKERS",
    "chat.giphyPicker.title": "GIPHY",
    "chat.giphyPicker.placeholder": "GIPHY के माध्यम से GIF खोजें",
    "chat.sendButton.ariaLabel": "संदेश भेजें",
    "chat.scrollDownButton.ariaLabel": "नीचे स्क्रॉल करें",
    "chat.stickerPicker.openButton.ariaLabel": "स्टिकर खोलो",
    "chat.giphyPicker.openButton.ariaLabel": "GIPHY खोलो",
    "chat.stickerPicker.closeButton.ariaLabel": "स्टिकर बंद करो",
    "chat.giphyPicker.closeButton.ariaLabel": "GIPHY बंद करो",
    "chat.stickerPicker.stickerPackTab.ariaLabel": "स्टिकर का पुलिंदा <packName>",
    "chat.stickerPicker.stickerSelectionButton.ariaLabel": "<stickerName> स्टिकर",
    "chat.giphyPicker.stickerSelectionButton.ariaLabel": "<stickerName> GIF",
    "chat.messageMenu.ariaLabel": "संदेश विकल्प",
    "chat.reactions.openButton.ariaLabel": "संदेश प्रतिक्रियाए",
    "chat.reactions.reactionSelectionButton.ariaLabel": "प्रतिक्रिया <reactionName>" 
  }
})
```

### Add a UI localization during initialization

Pass a localization object to the `localizedStrings`  argument of the `LiveLike.init` method to add localizations during initialization.

<Embed url="https://codepen.io/abhi1599/pen/QWgqRqK" href="https://codepen.io/abhi1599/pen/QWgqRqK" html="%3Ciframe%20height%3D'350'%20scrolling%3D'no'%20src%3D'https%3A%2F%2Fcodepen.io%2Fabhi1599%2Fembed%2FQWgqRqK'%20frameborder%3D'no'%20allowtransparency%3D'true'%20allowfullscreen%3D'true'%20style%3D'width%3A%20100%25%3B'%3E%3C%2Fiframe%3E" />

<br />

## Overriding UI localizations

Override localizations by passing a partial localization object to the `applyLocalization` method. It will merge the new localization object with any previously applied localizations.

```javascript
LiveLike.applyLocalization({
  en: {
    "widget.quiz.voteButton.label": "Submit",
    "widget.quiz.votedText": "Submitted!"
  }
})
```

## Setting the API request language

Some API responses can be localized too, such as widget details. Use the `LiveLike.setLanguage` method to set the language to make API requests with. If the response can be localized, it will use the supplied language.

```
LiveLike.setLanguage("en")
```

Under the hood, this will cause API requests to include the appropriate `Accept-Language` HTTP header.