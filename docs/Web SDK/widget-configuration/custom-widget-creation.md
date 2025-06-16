---
title: Custom Widget Creation
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Widget Creation | Web SDK | LiveLike
  description: >-
    Customizing widgets in Web SDK can be done by extending widget classes or
    creating custom templates. Learn more.
  robots: index
next:
  description: ''
---
There are two ways to customize widgets in the SDK - 
- *By extending widget classes*: This gives you full control over what you want to do with the widget, it is like creating a whole new widget using livelike widget as a base
- *By creating a custom template for a widget kind*: You define the template that gets returned from the livelike widget. You can add your own HTML tags in the template. Remove any component from the default widget template. We have various custom elements to help with the template building.
[block:api-header]
{
  "title": "Widget Classes"
}
[/block]
Widget classes can be extended to create any custom class which can be used to render widget instead of default widget. The available widget classes are:

- LiveLikePoll
- LiveLikeQuiz
- LiveLikePrediction
- LiveLikeFollowUp
- LiveLikeCheerMeter
- LiveLikeEmojiSlider
- LiveLikeRichPost
- LiveLikeSocialEmbed
- LiveLikeVideoAlert
- LiveLikeTextAsk
- LiveLikeNumberPrediction
- LiveLikeNumberFollowUp
[block:api-header]
{
  "title": "Custom Widget Rendering using classes"
}
[/block]
customElements can be defined from the classes created by extending livelike Widget Classes. These customElements can then be linked with the  livelike-widgets element using `customWidgetRenderer` method. The `customWidgetRenderer` method must return an HTMLTemplateElement, and the `widgetPayload` property is accessible as an argument
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/abhi1599/embed/wveNrdO' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/abhi1599/pen/wveNrdO",
  "title": "Custom Widget Rendering using classes",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico",
  "image": "https://assets.codepen.io/6912090/internal/screenshots/pens/wveNrdO.default.png?fit=cover&amp;format=auto&amp;ha=false&amp;height=360&amp;quality=75&amp;v=2&amp;version=1632913139&amp;width=640"
}
[/block]
Remember not to use default livelike widget elements which are the following:
- livelike-text-poll
- livelike-image-poll
- livelike-text-quiz
- livelike-image-quiz
- livelike-text-prediction
- livelike-text-prediction-follow-up
- livelike-image-prediction
- livelike-image-prediction-follow-up
- livelike-cheer-meter
- livelike-emoji-slider
- livelike-rich-post
- livelike-social-embed
- livelike-video-alert
- livelike-text-ask
- livelike-text-number-prediction
- livelike-text-number-prediction-follow-up
- livelike-image-number-prediction
- livelike-image-number-prediction-follow-up
[block:api-header]
{
  "title": "Custom Widget Rendering using classes for different presentation modes"
}
[/block]
Different UI can be defined for each presentation mode by using the mode property of the <livelike-widgets> element.

Here is an example with Number Prediction Widget custom UI only in interactive-timeline mode, for other modes stock UI is rendered by default.
[block:embed]
{
  "html": "<iframe height='350' scrolling='no' src='https://codepen.io/abhi1599/embed/eYEKEpb' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>",
  "url": "https://codepen.io/abhi1599/pen/eYEKEpb",
  "title": "Custom Widget Rendering using classes for different presentation modes",
  "favicon": "https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico"
}
[/block]

[block:api-header]
{
  "title": "Widget Templates"
}
[/block]
Widgets can be customized by creating a template element with a `kind` attribute to declare what kind of widget will be rendered. The available widget kinds are:

- text-poll
- image-poll
- text-quiz
- image-quiz
- text-prediction
- text-prediction-follow-up
- image-prediction
- image-prediction-follow-up
- cheer-meter
- emoji-slider
- rich-post
- social-embed
- video-alert
- text-ask
- text-number-prediction
- text-number-prediction-follow-up
- image-number-prediction
- image-number-prediction-follow-up

The children of the template element will get rendered inside of the widget. 

[block:code]
{
  "codes": [
    {
      "code": "<!-- Template -->\n<template kind=\"text-poll\">\n  <livelike-widget-root></livelike-widget-root>\n</template>\n\n<!-- What gets rendered -->\n<livelike-text-poll>\n  <livelike-widget-root></livelike-widget-root>\n</livelike-text-poll>",
      "language": "html",
      "name": "Widget template"
    }
  ]
}
[/block]
Once a template is rendered on the page, all widgets of that same `kind` will be rendered using that template's children, whether the widget is getting rendered from a single tag on the page, or from being published from the CMS. 

If you require multiple different template's to be rendered conditionally per widget kind, read the `Custom Template Rendering` section below.
[block:callout]
{
  "type": "warning",
  "body": "To write custom widget templates in JSX, one way would be to use the Higher Order Component below.\n\nFor extending widget classes, customElements can be. created by extending widget classes as shown below and then the file in which customElements have been defined needs to be imported in the react component where <livelike-widgets> is used",
  "title": "If using React, the template tag doesn't render in JSX the same way it does in HTML"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function Template({ children, ...attrs }) {\n  return <template {...attrs} dangerouslySetInnerHTML={{ __html: children }} />;\n}\n\n<Template kind=\"text-poll\">\n  {`<livelike-widget-root></livelike-widget-root>`}\n</Template>",
      "language": "javascript",
      "name": "JSX Template"
    },
    {
      "code": "import { html, LiveLikeAlert } from \"@livelike/engagementsdk\";\n\nclass CustomAlert extends LiveLikeAlert {\n  render() {\n    const hasCaptionAndMedia = !!this.text && !!this.image_url;\n\n    const hasOnlyMedia = !this.text && !!this.image_url;\n\n    const hasOnlyCaption = !!this.text && !this.image_url;\n\n    const paramsString = !!this.link_url && new URLSearchParams(this.link_url.split('?')[1]);\n\n    const hasSponsor = paramsString && paramsString.get(\"sponsor\");\n\n    return html`\n      <template>\n        <style>\n          livelike-widget-root.custom-widget livelike-widget-header{\n            background: white;\n            text-align: center;\n            display: block;\n            padding-bottom: 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-bottom: 0;\n          }\n          livelike-widget-root.custom-widget livelike-timer.custom-timer{\n            background: #fac83c;\n            top: 0;\n            height: 5px;\n          }\n          livelike-widget-root.custom-widget .widget-kind{\n            color: #000;\n            opacity: 30%;\n            font-size: 14.5px;\n            letter-spacing: 0.55px;\n            font-family: \"HelveticaNeue-Medium\";\n            padding: 15px 20px 0 20px;\n          }\n          livelike-widget-root.custom-widget livelike-title.custom-title{\n            color: #000;\n            font-size: 20px;\n            font-family: \"HelveticaNeue-Bold\";\n            padding: 0 20px;\n            display: block;\n            width: calc(100% - 40px);\n          }\n          livelike-widget-root.custom-widget livelike-widget-body{\n            background: white;\n            padding: 0 20px 20px 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-top: 0;\n          }\n          livelike-widget-root.custom-widget livelike-description{\n            font-size: 18.5px;\n            font-family: \"HelveticaNeue-Regular\";\n            text-align: left;\n          }\n          livelike-footer a.widget-link{\n            margin-top: 10px;\n            border-radius: 5px;\n            text-align: center;\n            color: white;\n            background-image: none;\n            padding: 1rem;\n            background-color: #222;\n          }\n          livelike-footer div.sponsor-section{\n            margin-top: 10px;\n            display: flex;\n            align-items: center;\n            justify-content: center;\n          }\n          livelike-footer div.sponsor-section span{\n            margin-right: 10px;\n            color: #bbbbbb;\n          }\n          livelike-footer div.sponsor-section img{\n            height: 30px;\n            width: auto;\n          }\n          .widget-caption{\n            color: #000;\n            opacity: 60%;\n          }\n          .widget-media img{\n            max-height: none;\n            height: auto;\n          }\n        </style>\n        <livelike-widget-root class=\"custom-widget\">\n          <livelike-widget-header class=\"widget-header\" slot=\"header\">\n            <livelike-timer class=\"custom-timer\"></livelike-timer>\n            <div class=\"widget-kind\">ALERT</div>\n            <livelike-title class=\"custom-title\"></livelike-title>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            ${hasCaptionAndMedia\n              ? html`\n                  <figure class=\"widget-captioned-media\">\n                    ${this.text &&\n                      html`\n                        <figcaption class=\"widget-caption media-caption\">\n                          ${this.text}\n                        </figcaption>\n                      `}\n                    ${this.image_url &&\n                      html`\n                        <img\n                          class=\"widget-media\"\n                          src=${this.image_url}\n                          alt=${this.text}\n                        />\n                      `}\n                  </figure>\n                `\n              : hasOnlyMedia\n              ? html`\n                  <div class=\"widget-media\">\n                    <img src=${this.image_url} />\n                  </div>\n                `\n              : hasOnlyCaption\n              ? html`\n                  <div class=\"widget-caption-container\">\n                    <span class=\"widget-caption\">${this.text}</span>\n                  </div>\n                `\n              : null}\n            ${this.link_url &&\n              html`\n                <livelike-footer>\n                  <a\n                    class=\"widget-link\"\n                    href=${this.link_url}\n                    target=\"_blank\"\n                    @click=${this.trackLinkOpened}\n                    >${this.link_label}</a>\n                    ${hasSponsor &&\n                      html`\n                        <div class=\"sponsor-section\">\n                          <span>Sponsored by</span>\n                          <img alt=\"sponsor logo\" src=\"https://cf-blast-storage-qa.livelikecdn.com/assets/7eea3117-20ce-455e-8996-9021e62245b1.png\"></img>\n                        </div>\n                    `}\n                </livelike-footer>\n              `}\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-alert\", CustomAlert);\n",
      "language": "javascript",
      "name": "Custom widget by extending class"
    },
    {
      "code": "import \"./custom-elements\";\nimport { useEffect } from 'react';\nimport LiveLike from \"@livelike/engagementsdk\";\n\nfunction App() {\n  useEffect(() => {\n    LiveLike.init({\n        clientId: 'xxxxxxxxxxxxxxxxxx'\n      }).then( p => {\n        const widgetContainer = document.querySelector('livelike-widgets');\n        widgetContainer.customWidgetRenderer = function({ widgetPayload }){\n          switch (widgetPayload.kind) {\n            case 'alert':\n              return document.createElement('custom-alert');\n            default:\n              break;\n          }\n        };\n      })\n  },[]);\n  return (\n    <div className=\"App\">\n      <livelike-widgets programid=\"xxxxxxxxxxxx\"></livelike-widgets>\n    </div>\n  );\n}\n\nexport default App;\n",
      "language": "javascript",
      "name": "React component using customElements"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Custom Template Rendering"
}
[/block]
Adding a template tag will render all widgets of that kind to have the markup of the template's children. To render different templates conditionally, the method `customTemplateRenderer` on the livelike-widgets element can be used. The `customTemplateRenderer` method must return an HTMLTemplateElement, and the `widgetPayload` property is accessible as an argument.  
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets></livelike-widgets>\n<template kind=\"alert\" id=\"customAlert\"></template>\n<template kind=\"cheer-meter\" id=\"customCheerMeter\"></template>\n\n<script>\nconst widgetContainer = document.querySelector('livelike-widgets');\nwidgetContainer.customTemplateRenderer = function({ widgetPayload }){\n  switch (widgetPayload.kind) {\n    case 'alert':\n      return document.querySelector('template#customAlert');\n    case 'cheer-meter':\n      return document.querySelector('template#customCheerMeter');\n      break;\n    default:\n      break;\n  }\n};\n</script>",
      "language": "html"
    }
  ]
}
[/block]
Properties from the `widgetPayload` can be used to create widgets in any way.
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets></livelike-widgets>\n\n<script>\nconst widgetContainer = document.querySelector('livelike-widgets');\n                                               \nfunction customImageAlert(widgetPayload){\n  const alertWidget = document.createElement('template');\n  alertWidget.innerHTML = `\n    <h2>${widgetPayload.title}</h2>\n    <img src=\"${widgetPayload.image_url}\" />\n\t\t<span>${widgetPayload.text}</span>\n  `;\n  return alertWidget;\n}\n\nwidgetContainer.customTemplateRenderer = function({ widgetPayload }){\n\tif(widgetPayload.kind === 'alert'){\n    if(widgetPayload.image_url){\n      return customImageAlert(widgetPayload);\n    }\n  }\n};\n</script>",
      "language": "html"
    }
  ]
}
[/block]