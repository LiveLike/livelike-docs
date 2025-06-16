---
title: Localization
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
As an integrator you have the ability to localize the EngagementSDK chat and widget experience. Multiple languages can be used, and they can be changed on the fly. 

These localizations are stored in the `localizedStrings` object, which has [ISO 639-1 Language Codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) as keys, and a value of an object of translations.
[block:api-header]
{
  "title": "Default Localization"
}
[/block]
The SDK comes with an English localisation by default. The default `localizedStrings` object is shown below.
[block:code]
{
  "codes": [
    {
      "code": "\"en\": {\n  \"chat.inputPlaceholder\": \"Say something...\",\n  \"chat.messageMenu.blockUser\": \"Block this user\",\n  \"chat.messageMenu.reportMessage\": \"Report message\",\n  \"chat.messageMenu.cancel\": \"Cancel\",\n  \"chat.messageMenu.ariaLabel\": \"Message options\",\n  \"chat.blockConfirmation.message\": \"You will no longer see messages from this user.\",\n  \"chat.reportConfirmation.message\": \"The message has been reported to the moderators. Thank you.\",\n  \"chat.mutedMessage\": \"Unable to send message.\",\n  \"chat.errorMessage\": \"There was an error. Please try again.\",\n  \"chat.messageDeleted\": \"This message has been removed.\",\n  \"chat.sendButton.ariaLabel\": \"Send Message\",\n  \"chat.scrollDownButton.ariaLabel\": \"Scroll Down\",\n  \"chat.stickerPicker.title\": \"STICKERS\",\n  \"chat.stickerPicker.openButton.ariaLabel\": \"Open Stickers\",\n  \"chat.stickerPicker.closeButton.ariaLabel\": \"Close Stickers\",\n  \"chat.stickerPicker.stickerPackTab.ariaLabel\": \"Sticker pack <packName>\",\n  \"chat.stickerPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> Sticker\",\n  \"chat.giphyPicker.title\": \"GIPHY\",\n  \"chat.giphyPicker.placeholder\": \"Search GIFs via GIPHY\",\n  \"chat.giphyPicker.openButton.ariaLabel\": \"Open GIPHY\",\n  \"chat.giphyPicker.closeButton.ariaLabel\": \"Close GIPHY\",\n  \"chat.giphyPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> GIF\",\n  \"chat.reactions.openButton.ariaLabel\": \"Message reactions\",\n  \"chat.reactions.reactionSelectionButton.ariaLabel\": \"Reaction <reactionName>\",\n  \"widget.quiz.voteButton.label\": \"Vote\",\n  \"widget.quiz.votedText\": \"Voted!\",\n  \"widget.slider.voteButton.label\": \"Vote\",\n  \"widget.slider.votedText\": \"Voted!\",\n  \"widget.textAsk.placeholder\": \"Type something...\",\n  \"widget.textAsk.sendButton.label\": \"SEND\",\n  \"widget.video.playbackError\": \"Can’t play this video\",\n  \"widget.sponsors.label\": \"Sponsored by\",\n  \"widget.quiz.tag\": \"\",\n  \"widget.poll.tag\": \"\",\n  \"widget.prediction.tag\": \"\",\n  \"widget.followup.tag\": \"\",\n}",
      "language": "javascript",
      "name": "Default localization"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Setting Custom Localizations"
}
[/block]
The `localizedStrings` object can be set by passing custom localizations to either the `LiveLike.init` method's `localizedStrings` argument, or the `LiveLike.applyLocalization` method.

## LiveLike.applyLocalization
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.applyLocalization({\n  hi: {\n    \"chat.inputPlaceholder\": \"कुछ बोलो...\",\n    \"chat.messageMenu.blockUser\": \"इस उपयोगकर्ता को ब्लॉक करें\",\n    \"chat.messageMenu.reportMessage\": \"रिपोर्ट संदेश\",\n    \"chat.messageMenu.cancel\": \"रद्द करें\",\n    \"chat.blockConfirmation.message\": \"अब आप <username> के संदेश नहीं देखेंगे\",\n    \"chat.reportConfirmation.message\": \"यह संदेश मध्यस्थों को सूचित किया गया है। धन्यवाद।\",\n    \"chat.errorMessage\": \"एक त्रुटि हुई। कृपया पुन: प्रयास करें।\",\n    \"chat.messageDeleted\": \"यह संदेश हटा दिया गया है।\",\n    \"chat.stickerPicker.title\": \"STICKERS\",\n    \"chat.giphyPicker.title\": \"GIPHY\",\n    \"chat.giphyPicker.placeholder\": \"GIPHY के माध्यम से GIF खोजें\",\n    \"chat.sendButton.ariaLabel\": \"संदेश भेजें\",\n    \"chat.scrollDownButton.ariaLabel\": \"नीचे स्क्रॉल करें\",\n    \"chat.stickerPicker.openButton.ariaLabel\": \"स्टिकर खोलो\",\n    \"chat.giphyPicker.openButton.ariaLabel\": \"GIPHY खोलो\",\n    \"chat.stickerPicker.closeButton.ariaLabel\": \"स्टिकर बंद करो\",\n    \"chat.giphyPicker.closeButton.ariaLabel\": \"GIPHY बंद करो\",\n    \"chat.stickerPicker.stickerPackTab.ariaLabel\": \"स्टिकर का पुलिंदा <packName>\",\n    \"chat.stickerPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> स्टिकर\",\n    \"chat.giphyPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> GIF\",\n    \"chat.messageMenu.ariaLabel\": \"संदेश विकल्प\",\n    \"chat.reactions.openButton.ariaLabel\": \"संदेश प्रतिक्रियाए\",\n    \"chat.reactions.reactionSelectionButton.ariaLabel\": \"प्रतिक्रिया <reactionName>\" \n  }\n})",
      "language": "javascript"
    }
  ]
}
[/block]
## LiveLike.init argument
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/abhi1599/embed/QWgqRqK' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/abhi1599/pen/QWgqRqK",
  "title": "Localization LiveLike.init argument",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico"
}
[/block]

[block:api-header]
{
  "title": "Usage"
}
[/block]
The keys of `localizedStrings` are valid language codes, and they will match the [`lang` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang) used in HTML tags.

## Single language

For example, if a Spanish localization is used, the language code is `es`. The `es` language code will be used as both the `localizedStrings` key, and the `lang` attribute.
[block:code]
{
  "codes": [
    {
      "code": "<livelike-chat lang=\"es\" roomid=\"\"></livelike-chat>\n<script>\nLiveLike.init({\n  clientId: '',\n  localizedStrings: {\n    es: {\n      \"chat.inputPlaceholder\": \"Dices Algo\",\n      \"chat.messageMenu.blockUser\": \"Bloquea a esta persona\",\n      \"chat.messageMenu.reportMessage\": \"Reporte este mensaje\",\n      \"chat.messageMenu.cancel\": \"Cancelar\",\n      \"chat.messageMenu.ariaLabel\": \"Opciones de mensaje\",\n      \"chat.blockConfirmation.message\": \"Ya no recibirás mensajes de <username>.\",\n      \"chat.reportConfirmation.message\": \"El mensaje ha sido informado a los moderadores. Gracias.\",\n      \"chat.errorMessage\": \"Hubo un error. Inténtalo de nuevo.\",\n      \"chat.messageDeleted\": \"Este mensaje ha sido eliminado.\",\n      \"chat.sendButton.ariaLabel\": \"Enviar mensaje\",\n      \"chat.scrollDownButton.ariaLabel\": \"Desplazarse hacia abajo\",\n      \"chat.stickerPicker.title\": \"Pegatinas\",\n      \"chat.stickerPicker.openButton.ariaLabel\": \"Abrir pegatinas\",\n      \"chat.stickerPicker.closeButton.ariaLabel\": \"Cerrar pegatinas\",\n      \"chat.stickerPicker.stickerPackTab.ariaLabel\": \"Paquete de pegatinas <packName>\",\n      \"chat.stickerPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> pegatina\",\n      \"chat.giphyPicker.title\": \"GIPHY\",\n      \"chat.giphyPicker.placeholder\": \"Buscar GIF a través de GIPHY\",\n      \"chat.giphyPicker.openButton.ariaLabel\": \"Abrir GIPHY\",\n      \"chat.giphyPicker.closeButton.ariaLabel\": \"Cerrar GIPHY\",\n      \"chat.giphyPicker.stickerSelectionButton.ariaLabel\": \"<stickerName> GIF\",\n      \"chat.reactions.openButton.ariaLabel\": \"Reacciones de mensajes\",\n      \"chat.reactions.reactionSelectionButton.ariaLabel\": \"Reacción <reactionName>\"\n  \t}\n  }       \n})\n</script>",
      "language": "html"
    }
  ]
}
[/block]
## Multiple Languages

Multiple language keys can be added to the `localizedStrings` object. These languages can then be dynamically changed in your application.

## Limited Keys
Integrators can override default values by setting the keys they want to change. 
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.applyLocalization({\n  en: {\n    \"widget.quiz.voteButton.label\": \"Submit\",\n    \"widget.quiz.votedText\": \"Submitted!\"\n  }\n})",
      "language": "javascript"
    }
  ]
}
[/block]