---
title: Custom Widget Examples
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Widget Examples | Web SDK | LiveLike
  description: >-
    Customize your widgets to make them suit your unique brand. See custom
    alerts, quizzes, cheer meters, predictions, and more.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Alert Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "0-1": "string",
    "0-0": "title",
    "1-0": "text",
    "2-0": "image_url",
    "3-0": "link_url",
    "4-0": "link_label",
    "1-1": "string",
    "2-1": "string",
    "3-1": "string",
    "4-1": "string",
    "5-0": "trackLinkOpened",
    "5-1": "function: ()"
  },
  "cols": 2,
  "rows": 6
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "const alertTemplate = (payload) => {\n  var template = document.createElement('template');\n  let alertHtml = `\n    <livelike-widget-root>\n      <livelike-widget-header>\n        <livelike-title>${payload.title}</livelike-title>\n      </livelike-widget-header>\n      <livelike-widget-body>\n        <img src=${payload.image_url}>\n      \t<a href=\"${payload.link_url}\" target=\"_blank\">${payload.link_label}</a>\n      </livelike-widget-body>\n    </livelike-widget-root>\n  `;\n  template.innerHTML = alertHtml;\n  return template;\n}\nconst widgetContainer = document.querySelector('livelike-widgets');\nwidgetContainer.customTemplateRenderer = function({ widgetPayload }){\n  if(widgetPayload.kind === 'alert'){\n    return alertTemplate(widgetPayload);\n  }\n}\n",
      "language": "javascript",
      "name": "Alert Widget Example"
    },
    {
      "code": "class CustomAlert extends LiveLikeAlert {\n      render() {\n        return html`\n          <template>\n            <livelike-widget-root>\n              <livelike-widget-header>\n              <livelike-title></livelike-title>\n                ${this.link_url &&\n                html`\n                  <a href=\"${this.link_url}\" target=\"_blank\">${this.link_label}</a>\n                `}\n              </livelike-widget-header>\n              <livelike-widget-body>\n                <span>${this.text}</span>\n                ${this.image_url &&\n                html`\n                  <img src=${this.image_url} height=\"40px\">\n                `}\n              </livelike-widget-body>\n            </livelike-widget-root>\n          <template>\n        `;\n      }\n    }\n    customElements.define(\"custom-alert\", CustomAlert);\n    \nconst customWidgetRenderer = (args) => {\n      let widgetPayload = args.widgetPayload;\n      if( widgetPayload.kind === 'alert'){\n        return document.createElement('custom-alert');\n      }\n    }\nlet w = document.querySelector('livelike-widgets');\nw.customWidgetRenderer = customWidgetRenderer;",
      "language": "text",
      "name": "Extended Alert Class"
    },
    {
      "code": "class CustomAlert extends LiveLikeAlert {\n  render() {\n    const hasCaptionAndMedia = !!this.text && !!this.image_url;\n\n    const hasOnlyMedia = !this.text && !!this.image_url;\n\n    const hasOnlyCaption = !!this.text && !this.image_url;\n\n    const paramsString = !!this.link_url && new URLSearchParams(this.link_url.split('?')[1]);\n\n    const hasSponsor = paramsString && paramsString.get(\"sponsor\");\n\n    return html`\n      <template>\n        <style>\n        \tlivelike-widget-root.custom-widget livelike-widget-header{\n            background: white;\n            text-align: center;\n            display: block;\n            padding-bottom: 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-bottom: 0;\n          }\n          livelike-widget-root.custom-widget livelike-timer.custom-timer{\n            background: #fac83c;\n            top: 0;\n            height: 5px;\n          }\n          livelike-widget-root.custom-widget .widget-kind{\n            color: #000;\n            opacity: 30%;\n            font-size: 14.5px;\n            letter-spacing: 0.55px;\n            font-family: \"HelveticaNeue-Medium\";\n            padding: 15px 20px 0 20px;\n          }\n          livelike-widget-root.custom-widget livelike-title.custom-title{\n            color: #000;\n            font-size: 20px;\n            font-family: \"HelveticaNeue-Bold\";\n            padding: 0 20px;\n            display: block;\n            width: calc(100% - 40px);\n          }\n          livelike-widget-root.custom-widget livelike-widget-body{\n            background: white;\n            padding: 0 20px 20px 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-top: 0;\n          }\t\n          livelike-widget-root.custom-widget livelike-description{\n            font-size: 18.5px;\n            font-family: \"HelveticaNeue-Regular\";\n            text-align: left;\n          }\n          livelike-footer a.widget-link{\n            margin-top: 10px;\n            border-radius: 5px;\n            text-align: center;\n            color: white;\n            background-image: none;\n            padding: 1rem;\n            background-color: #222;\n          }\n          livelike-footer div.sponsor-section{\n            margin-top: 10px;\n            display: flex;\n            align-items: center;\n            justify-content: center;\n          }\n          livelike-footer div.sponsor-section span{\n            margin-right: 10px;\n            color: #bbbbbb;\n          }\n          livelike-footer div.sponsor-section img{\n            height: 30px;\n            width: auto;\n          }\n          .widget-caption{\n            color: #000;\n            opacity: 60%;\n          }\n          .widget-media img{\n            max-height: none;\n            height: auto;\n          }\n        </style>\n        <livelike-widget-root class=\"custom-widget\">\n          <livelike-widget-header class=\"widget-header\" slot=\"header\">\n            <livelike-timer class=\"custom-timer\"></livelike-timer>\n            <div class=\"widget-kind\">ALERT</div>\n            <livelike-title class=\"custom-title\"></livelike-title>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            ${hasCaptionAndMedia\n              ? html`\n                  <figure class=\"widget-captioned-media\">\n                    ${this.text &&\n                      html`\n                        <figcaption class=\"widget-caption media-caption\">\n                          ${this.text}\n                        </figcaption>\n                      `}\n                    ${this.image_url &&\n                      html`\n                        <img\n                          class=\"widget-media\"\n                          src=${this.image_url}\n                          alt=${this.text}\n                        />\n                      `}\n                  </figure>\n                `\n              : hasOnlyMedia\n              ? html`\n                  <div class=\"widget-media\">\n                    <img src=${this.image_url} />\n                  </div>\n                `\n              : hasOnlyCaption\n              ? html`\n                  <div class=\"widget-caption-container\">\n                    <span class=\"widget-caption\">${this.text}</span>\n                  </div>\n                `\n              : null}\n            ${this.link_url &&\n              html`\n                <livelike-footer>\n                  <a\n                    class=\"widget-link\"\n                    href=${this.link_url}\n                    target=\"_blank\"\n                    @click=${this.trackLinkOpened}\n                    >${this.link_label}</a>\n                    ${hasSponsor &&\n                      html`\n                        <div class=\"sponsor-section\">\n                          <span>Sponsored by</span>\n                          <img alt=\"sponsor logo\" src=\"https://cf-blast-storage-qa.livelikecdn.com/assets/7eea3117-20ce-455e-8996-9021e62245b1.png\"></img>\n                        </div>\n                    `}\n                </livelike-footer>\n              `}\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-alert\", CustomAlert);\nconst widgetContainer = document.querySelector('livelike-widgets');\n\twidgetContainer.customWidgetRenderer = function({ widgetPayload }){\n  switch (widgetPayload.kind) {\n    case 'alert':\n      return document.createElement('custom-alert');\n    default:\n      break;\n  }\n};",
      "language": "javascript",
      "name": "Custom Alert Widget"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Quiz Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "question",
    "0-1": "question",
    "1-0": "choices",
    "1-1": "array",
    "h-0": "Property",
    "h-1": "Type",
    "2-0": "lockInVote",
    "2-1": "function: (option)"
  },
  "cols": 2,
  "rows": 3
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<template kind=\"text-quiz\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n      <livelike-dismiss-button></livelike-dismiss-button>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Quiz Widget Example"
    },
    {
      "code": "<style>\n  livelike-widget-root.custom-widget livelike-widget-header{\n    background: white;\n    text-align: center;\n    display: block;\n    padding-bottom: 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-bottom: 0;\n  }\n  livelike-widget-root.custom-widget livelike-timer.custom-timer{\n    background: #fac83c;\n    top: 0;\n    height: 5px;\n  }\n  livelike-widget-root.custom-widget .widget-kind{\n    color: #000;\n    opacity: 30%;\n    font-size: 14.5px;\n    letter-spacing: 0.55px;\n    font-family: \"HelveticaNeue-Medium\";\n    padding: 15px 20px 0 20px;\n  }\n  livelike-widget-root.custom-widget livelike-title.custom-title{\n    color: #000;\n    font-size: 20px;\n    font-family: \"HelveticaNeue-Bold\";\n    padding: 0 20px;\n    display: block;\n    width: calc(100% - 40px);\n  }\n  livelike-widget-root.custom-widget livelike-widget-body{\n    background: white;\n    padding: 0 20px 20px 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-top: 0;\n  }\n  livelike-widget-root.custom-widget livelike-select{\n    background: #fff;\n  }\n  livelike-widget-root.custom-widget livelike-option{\n    color: #000;\n    border: 1px solid #e6e6e6;\n    padding: 0;\n    margin-bottom: 20px;\n    height: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option:last-child{\n    margin-bottom: 0px;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected]{\n    color: #fff;\n    background: #000;\n  }\n  livelike-widget-root.custom-widget livelike-description{\n    font-size: 18.5px;\n    font-family: \"HelveticaNeue-Regular\";\n    text-align: left;\n  }\n  livelike-widget-root.custom-widget livelike-percentage{\n    font-size: 21px;\n    font-family: \"HelveticaNeue-CondensedBlack\"\n  }\n  livelike-widget-root.custom-widget livelike-progress{\n    height: 4px;\n    bottom: 0;\n    top: auto;\n    background: #e6e6e6;\n    border-color: #e6e6e6;\n    border-radius: 0;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n    background: #0096ff;\n    border-color: #0096ff;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid{\n    display: grid;\n    grid-template-columns: repeat(2, 1fr);\n    grid-column-gap: 15px;\n    grid-row-gap: 10px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{\n    margin-bottom: 0;\n    min-height: 60px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n    width: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{\n    flex-grow: 1;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{\n    background: #00ff78;\n    border-color: #00ff78;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{\n    background: #ff3c3c;\n    border-color: #ff3c3c;\n  }\n</style>\n<template kind=\"image-quiz\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">IMAGE QUIZ</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select class=\"image-grid\">\n        <template>\n          <livelike-option>\n            <div class=\"livelike-voting-image-container\">\n              <div class=\"image-description-wrapper\">\n                <livelike-description></livelike-description>\n              </div>\n              <livelike-percentage></livelike-percentage>\n            </div>\n            <livelike-image height=\"60px\"></livelike-image>\n            <livelike-progress></livelike-progress>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Custom Image Quiz"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Cheer Meter Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "title",
    "0-1": "string",
    "1-0": "options",
    "1-1": "array",
    "h-0": "Property",
    "h-1": "Type",
    "2-0": "submitVote",
    "2-1": "function: (option)"
  },
  "cols": 2,
  "rows": 3
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<template kind=\"cheer-meter\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-dismiss-button></livelike-dismiss-button>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select>\n        <template>\n          <livelike-option>\n            <livelike-vote-count></livelike-vote-count>\n            <livelike-description></livelike-description>\n            <livelike-image height=\"50px\" width=\"50px\"></livelike-image>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Cheer Meter Example"
    },
    {
      "code": "<script>\n  class CustomCheerOption extends LiveLikeOption {\n    votePercentage = () => {\n      const totalVotes = this.items.reduce((a, b) => a + b['vote_count'], 0);\n      return totalVotes > 0\n        ? Math.round((this.item.vote_count / totalVotes) * 100)\n        : 0;\n    };\n    render() {\n      return html`\n        <style>\n          livelike-image{\n            width: calc(100% - 42px);\n            padding: 20px;\n            border: 1px solid #e6e6e6;\n            border-radius: 6px;\n            flex-grow: 1;\n          }\n          :host(:not([disabled])) livelike-image:active{\n            background-color: #222222 !important;\n          }\n          livelike-description{\n            font-size: 18.5px;\n            font-family: \"HelveticaNeue-Regular\";\n            text-align: center;\n            flex-grow: 0;\n          }\n        </style>\n        <livelike-image width=\"100%\" height=\"auto\" style=\"background: linear-gradient(0deg, ${this.optionIndex % 2 === 0 ? `#0096ff` : `#ed174b` } ${this.votePercentage()}%, transparent 0);\"></livelike-image>\n        <livelike-description></livelike-description>\n      `;\n    }\n}\ncustomElements.define(\"custom-cheer-option\", CustomCheerOption);\n</script>\n<style>\n  body{\n  background-color: #f0f0f0;\n}\nlivelike-widgets{\n  width: 500px;\n  height: 340px;\n  margin-left: auto;\n  margin-right: auto;\n}\nlivelike-widget-root.custom-widget livelike-widget-header{\n  background: white;\n  text-align: center;\n  display: block;\n  padding-bottom: 20px;\n  border-radius: 0;\n  border: 1px solid #e6e6e6;\n  border-bottom: 0;\n}\nlivelike-widget-root.custom-widget livelike-timer.custom-timer{\n  background: #fac83c;\n  top: 0;\n  height: 5px;\n}\nlivelike-widget-root.custom-widget .widget-kind{\n  color: #000;\n  opacity: 30%;\n  font-size: 14.5px;\n  letter-spacing: 0.55px;\n  font-family: \"HelveticaNeue-Medium\";\n  padding: 15px 20px 0 20px;\n}\nlivelike-widget-root.custom-widget livelike-title.custom-title{\n  color: #000;\n  font-size: 20px;\n  font-family: \"HelveticaNeue-Bold\";\n  padding: 0 20px;\n  display: block;\n  width: calc(100% - 40px);\n}\nlivelike-widget-root.custom-widget livelike-widget-body{\n  background: white;\n  padding: 0 20px 20px 20px;\n  border-radius: 0;\n  border: 1px solid #e6e6e6;\n  border-top: 0;\n}\nlivelike-widget-root.custom-widget livelike-select{\n  background: #fff;\n}\nlivelike-widget-root.custom-widget livelike-option{\n  color: #000;\n  border: 1px solid #e6e6e6;\n  padding: 0;\n  margin-bottom: 20px;\n  height: auto;\n}\nlivelike-widget-root.custom-widget livelike-option:last-child{\n  margin-bottom: 0px;\n}\nlivelike-widget-root.custom-widget livelike-option[selected]{\n  color: #fff;\n  background: #000;\n}\nlivelike-widget-root.custom-widget livelike-description{\n  font-size: 18.5px;\n  font-family: \"HelveticaNeue-Regular\";\n  text-align: left;\n}\nlivelike-widget-root.custom-widget livelike-percentage{\n  font-size: 21px;\n  font-family: \"HelveticaNeue-CondensedBlack\"\n}\nlivelike-widget-root.custom-widget livelike-progress{\n  height: 4px;\n  bottom: 0;\n  top: auto;\n  background: #e6e6e6;\n  border-color: #e6e6e6;\n  border-radius: 0;\n}\nlivelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n  background: #0096ff;\n  border-color: #0096ff;\n}\nlivelike-widget-root.custom-widget livelike-select.image-grid{\n  display: grid;\n  grid-template-columns: repeat(2, 1fr);\n  grid-column-gap: 15px;\n  grid-row-gap: 10px;\n}\nlivelike-widget-root.custom-widget livelike-select.image-grid livelike-option{\n  margin-bottom: 0;\n  min-height: 60px;\n}\nlivelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n  width: auto;\n}\nlivelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{\n  flex-grow: 1;\n}\nlivelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{\n  background: #00ff78;\n  border-color: #00ff78;\n}\nlivelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{\n  background: #ff3c3c;\n  border-color: #ff3c3c;\n}\nlivelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid{\n  width: 100%;\n  background: transparent;\n  display: flex;\n  justify-content: space-around;\n}\nlivelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid custom-cheer-option{\n  display: flex;\n  flex-direction: column;\n  border: none;\n  margin-bottom: 0;\n  min-height: 60px;\n  color: #000;\n  padding: 0;\n  height: auto;\n  width: 100px;\n}\nlivelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n  width: calc(100% - 22px);\n  padding: 10px;\n  border: 1px solid #e6e6e6;\n  border-radius: 6px;\n}\nlivelike-cheer-meter livelike-widget-root.custom-widget img.divider{\n  color: #000;\n  position: absolute;\n  top: 50%;\n  left: 50%;\n  transform: translate(-50%, -50%);\n  font-size: 2rem;\n  z-index: 100;\n}\nlivelike-cheer-meter livelike-widget-root.custom-widget livelike-description{\n  text-align: center;\n}\n</style>\n<template kind=\"cheer-meter\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">CHEER METER</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <div class=\"cheer-image-body\">\n        <livelike-vote-count></livelike-vote-count>\n        <img class=\"divider\" src=\"./assets/vs-light.gif\" />\n        <livelike-select class=\"image-grid\">\n          <template>\n            <custom-cheer-option></custom-cheer-option>\n          </template>\n        </livelike-select>\n      </div>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Custom Cheer Meter"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Prediction Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "0-0": "question",
    "0-1": "string",
    "1-0": "options",
    "1-1": "array",
    "2-0": "submitVote",
    "2-1": "function: (option)"
  },
  "cols": 2,
  "rows": 3
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<template kind=\"text-prediction\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>\n<template kind=\"image-prediction\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-image height=\"60px\"></livelike-image>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Prediction widgets"
    },
    {
      "code": "<template kind=\"text-prediction-follow-up\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>\n<template kind=\"image-prediction-follow-up\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-image height=\"60px\"></livelike-image>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Follow-ups"
    },
    {
      "code": "<style>\n  livelike-widget-root.custom-widget livelike-widget-header{\n    background: white;\n    text-align: center;\n    display: block;\n    padding-bottom: 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-bottom: 0;\n  }\n  livelike-widget-root.custom-widget livelike-timer.custom-timer{\n    background: #fac83c;\n    top: 0;\n    height: 5px;\n  }\n  livelike-widget-root.custom-widget .widget-kind{\n    color: #000;\n    opacity: 30%;\n    font-size: 14.5px;\n    letter-spacing: 0.55px;\n    font-family: \"HelveticaNeue-Medium\";\n    padding: 15px 20px 0 20px;\n  }\n  livelike-widget-root.custom-widget livelike-title.custom-title{\n    color: #000;\n    font-size: 20px;\n    font-family: \"HelveticaNeue-Bold\";\n    padding: 0 20px;\n    display: block;\n    width: calc(100% - 40px);\n  }\n  livelike-widget-root.custom-widget livelike-widget-body{\n    background: white;\n    padding: 0 20px 20px 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-top: 0;\n  }\n  livelike-widget-root.custom-widget livelike-select{\n    background: #fff;\n  }\n  livelike-widget-root.custom-widget livelike-option{\n    color: #000;\n    border: 1px solid #e6e6e6;\n    padding: 0;\n    margin-bottom: 20px;\n    height: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option:last-child{\n    margin-bottom: 0px;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected]{\n    color: #fff;\n    background: #000;\n  }\n  livelike-widget-root.custom-widget livelike-description{\n    font-size: 18.5px;\n    font-family: \"HelveticaNeue-Regular\";\n    text-align: left;\n  }\n  livelike-widget-root.custom-widget livelike-percentage{\n    font-size: 21px;\n    font-family: \"HelveticaNeue-CondensedBlack\"\n  }\n  livelike-widget-root.custom-widget livelike-progress{\n    height: 4px;\n    bottom: 0;\n    top: auto;\n    background: #e6e6e6;\n    border-color: #e6e6e6;\n    border-radius: 0;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n    background: #0096ff;\n    border-color: #0096ff;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid{\n    display: grid;\n    grid-template-columns: repeat(2, 1fr);\n    grid-column-gap: 15px;\n    grid-row-gap: 10px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{\n    margin-bottom: 0;\n    min-height: 60px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n    width: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{\n    flex-grow: 1;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{\n    background: #00ff78;\n    border-color: #00ff78;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{\n    background: #ff3c3c;\n    border-color: #ff3c3c;\n  }\n</style>\n<template kind=\"image-prediction\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">IMAGE PREDICTION</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select class=\"image-grid prediction-widget\">\n        <template>\n          <livelike-option>\n            <div class=\"livelike-voting-image-container\">\n              <div class=\"image-description-wrapper\">\n                <livelike-description></livelike-description>\n              </div>\n              <livelike-percentage></livelike-percentage>\n            </div>\n            <livelike-image height=\"60px\"></livelike-image>\n            <livelike-progress></livelike-progress>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Custom Image Prediction"
    },
    {
      "code": "<style>\n  livelike-widget-root.custom-widget livelike-widget-header{\n    background: white;\n    text-align: center;\n    display: block;\n    padding-bottom: 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-bottom: 0;\n  }\n  livelike-widget-root.custom-widget livelike-timer.custom-timer{\n    background: #fac83c;\n    top: 0;\n    height: 5px;\n  }\n  livelike-widget-root.custom-widget .widget-kind{\n    color: #000;\n    opacity: 30%;\n    font-size: 14.5px;\n    letter-spacing: 0.55px;\n    font-family: \"HelveticaNeue-Medium\";\n    padding: 15px 20px 0 20px;\n  }\n  livelike-widget-root.custom-widget livelike-title.custom-title{\n    color: #000;\n    font-size: 20px;\n    font-family: \"HelveticaNeue-Bold\";\n    padding: 0 20px;\n    display: block;\n    width: calc(100% - 40px);\n  }\n  livelike-widget-root.custom-widget livelike-widget-body{\n    background: white;\n    padding: 0 20px 20px 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-top: 0;\n  }\n  livelike-widget-root.custom-widget livelike-select{\n    background: #fff;\n  }\n  livelike-widget-root.custom-widget livelike-option{\n    color: #000;\n    border: 1px solid #e6e6e6;\n    padding: 0;\n    margin-bottom: 20px;\n    height: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option:last-child{\n    margin-bottom: 0px;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected]{\n    color: #fff;\n    background: #000;\n  }\n  livelike-widget-root.custom-widget livelike-description{\n    font-size: 18.5px;\n    font-family: \"HelveticaNeue-Regular\";\n    text-align: left;\n  }\n  livelike-widget-root.custom-widget livelike-percentage{\n    font-size: 21px;\n    font-family: \"HelveticaNeue-CondensedBlack\"\n  }\n  livelike-widget-root.custom-widget livelike-progress{\n    height: 4px;\n    bottom: 0;\n    top: auto;\n    background: #e6e6e6;\n    border-color: #e6e6e6;\n    border-radius: 0;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n    background: #0096ff;\n    border-color: #0096ff;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid{\n    display: grid;\n    grid-template-columns: repeat(2, 1fr);\n    grid-column-gap: 15px;\n    grid-row-gap: 10px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{\n    margin-bottom: 0;\n    min-height: 60px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n    width: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{\n    flex-grow: 1;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{\n    background: #00ff78;\n    border-color: #00ff78;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{\n    background: #ff3c3c;\n    border-color: #ff3c3c;\n  }\n</style>\n<template kind=\"image-prediction-follow-up\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">IMAGE PREDICTION FOLLOW UP</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select class=\"image-grid\">\n        <template>\n          <livelike-option>\n            <div class=\"livelike-voting-image-container\">\n              <div class=\"image-description-wrapper\">\n                <livelike-description></livelike-description>\n              </div>\n              <livelike-percentage></livelike-percentage>\n            </div>\n            <livelike-image height=\"60px\"></livelike-image>\n            <livelike-progress></livelike-progress>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Custom Image Prediction Follow Up"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Poll Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "question",
    "1-0": "options",
    "0-1": "string",
    "1-1": "array",
    "h-0": "Property",
    "h-1": "Type",
    "2-1": "function: (option)",
    "2-0": "submitVote"
  },
  "cols": 2,
  "rows": 3
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<template kind=\"text-poll\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>\n<template kind=\"image-poll\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n    </livelike-widget-header>\n    <livelike-select>\n      <template>\n        <livelike-option>\n          <livelike-image height=\"60px\"></livelike-image>\n          <livelike-description></livelike-description>\n          <livelike-percentage></livelike-percentage>\n          <livelike-vote-count></livelike-vote-count>\n        </livelike-option>\n      </template>\n    </livelike-select>\n  </livelike-widget-root>\n</template>",
      "language": "text"
    },
    {
      "code": "<style>\n  livelike-widget-root.custom-widget livelike-widget-header{\n    background: white;\n    text-align: center;\n    display: block;\n    padding-bottom: 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-bottom: 0;\n  }\n  livelike-widget-root.custom-widget livelike-timer.custom-timer{\n    background: #fac83c;\n    top: 0;\n    height: 5px;\n  }\n  livelike-widget-root.custom-widget .widget-kind{\n    color: #000;\n    opacity: 30%;\n    font-size: 14.5px;\n    letter-spacing: 0.55px;\n    font-family: \"HelveticaNeue-Medium\";\n    padding: 15px 20px 0 20px;\n  }\n  livelike-widget-root.custom-widget livelike-title.custom-title{\n    color: #000;\n    font-size: 20px;\n    font-family: \"HelveticaNeue-Bold\";\n    padding: 0 20px;\n    display: block;\n    width: calc(100% - 40px);\n  }\n  livelike-widget-root.custom-widget livelike-widget-body{\n    background: white;\n    padding: 0 20px 20px 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-top: 0;\n  }\n  livelike-widget-root.custom-widget livelike-select{\n    background: #fff;\n  }\n  livelike-widget-root.custom-widget livelike-option{\n    color: #000;\n    border: 1px solid #e6e6e6;\n    padding: 0;\n    margin-bottom: 20px;\n    height: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option:last-child{\n    margin-bottom: 0px;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected]{\n    color: #fff;\n    background: #000;\n  }\n  livelike-widget-root.custom-widget livelike-description{\n    font-size: 18.5px;\n    font-family: \"HelveticaNeue-Regular\";\n    text-align: left;\n  }\n  livelike-widget-root.custom-widget livelike-percentage{\n    font-size: 21px;\n    font-family: \"HelveticaNeue-CondensedBlack\"\n  }\n  livelike-widget-root.custom-widget livelike-progress{\n    height: 4px;\n    bottom: 0;\n    top: auto;\n    background: #e6e6e6;\n    border-color: #e6e6e6;\n    border-radius: 0;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n    background: #0096ff;\n    border-color: #0096ff;\n  }\n</style>\n<template kind=\"text-poll\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">TEXT POLL</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select>\n        <template>\n          <livelike-option>\n            <div style=\"width:100%;display:flex;align-items:center;\">\n              <livelike-progress></livelike-progress>\n              <livelike-description></livelike-description>\n              <livelike-percentage></livelike-percentage>\n            </div>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Customized Text Poll"
    },
    {
      "code": "<style>\n  livelike-widget-root.custom-widget livelike-widget-header{\n    background: white;\n    text-align: center;\n    display: block;\n    padding-bottom: 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-bottom: 0;\n  }\n  livelike-widget-root.custom-widget livelike-timer.custom-timer{\n    background: #fac83c;\n    top: 0;\n    height: 5px;\n  }\n  livelike-widget-root.custom-widget .widget-kind{\n    color: #000;\n    opacity: 30%;\n    font-size: 14.5px;\n    letter-spacing: 0.55px;\n    font-family: \"HelveticaNeue-Medium\";\n    padding: 15px 20px 0 20px;\n  }\n  livelike-widget-root.custom-widget livelike-title.custom-title{\n    color: #000;\n    font-size: 20px;\n    font-family: \"HelveticaNeue-Bold\";\n    padding: 0 20px;\n    display: block;\n    width: calc(100% - 40px);\n  }\n  livelike-widget-root.custom-widget livelike-widget-body{\n    background: white;\n    padding: 0 20px 20px 20px;\n    border-radius: 0;\n    border: 1px solid #e6e6e6;\n    border-top: 0;\n  }\n  livelike-widget-root.custom-widget livelike-select{\n    background: #fff;\n  }\n  livelike-widget-root.custom-widget livelike-option{\n    color: #000;\n    border: 1px solid #e6e6e6;\n    padding: 0;\n    margin-bottom: 20px;\n    height: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option:last-child{\n    margin-bottom: 0px;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected]{\n    color: #fff;\n    background: #000;\n  }\n  livelike-widget-root.custom-widget livelike-description{\n    font-size: 18.5px;\n    font-family: \"HelveticaNeue-Regular\";\n    text-align: left;\n  }\n  livelike-widget-root.custom-widget livelike-percentage{\n    font-size: 21px;\n    font-family: \"HelveticaNeue-CondensedBlack\"\n  }\n  livelike-widget-root.custom-widget livelike-progress{\n    height: 4px;\n    bottom: 0;\n    top: auto;\n    background: #e6e6e6;\n    border-color: #e6e6e6;\n    border-radius: 0;\n  }\n  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{\n    background: #0096ff;\n    border-color: #0096ff;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid{\n    display: grid;\n    grid-template-columns: repeat(2, 1fr);\n    grid-column-gap: 15px;\n    grid-row-gap: 10px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{\n    margin-bottom: 0;\n    min-height: 60px;\n  }\n  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{\n    width: auto;\n  }\n  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{\n    flex-grow: 1;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{\n    background: #00ff78;\n    border-color: #00ff78;\n  }\n  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{\n    background: #ff3c3c;\n    border-color: #ff3c3c;\n  }\n</style>\n<template kind=\"image-poll\">\n  <livelike-widget-root class=\"custom-widget\">\n    <livelike-widget-header class=\"widget-header\" slot=\"header\">\n      <livelike-timer class=\"custom-timer\"></livelike-timer>\n      <div class=\"widget-kind\">IMAGE POLL</div>\n      <livelike-title class=\"custom-title\"></livelike-title>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select class=\"image-grid\">\n        <template>\n          <livelike-option>\n            <div class=\"livelike-voting-image-container\">\n              <div class=\"image-description-wrapper\">\n                <livelike-description></livelike-description>\n              </div>\n              <livelike-percentage></livelike-percentage>\n            </div>\n            <livelike-image height=\"60px\"></livelike-image>\n            <livelike-progress></livelike-progress>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html",
      "name": "Customized Image Poll"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Slider Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "0-0": "question",
    "1-0": "options",
    "2-0": "average_magnitude",
    "3-0": "initial_magnitude",
    "0-1": "string",
    "2-1": "string",
    "3-1": "string",
    "1-1": "array",
    "4-0": "lockInVote",
    "4-1": "function: (magnitude: number)"
  },
  "cols": 2,
  "rows": 5
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomSlider extends LiveLikeEmojiSlider {\n      submitButtonClicked = () => {\n        let mag = this.querySelector('#magnitude-input').value;\n        this.submitResults(mag).then((r) => console.log('slider vote submitted', r));\n      }\n      render() {\n        return html`\n          <template>\n            <livelike-widget-root>\n              <livelike-widget-header>\n                <livelike-title slot=\"title\"></livelike-title>\n                <livelike-dismiss-button slot=\"dismiss\"></livelike-dismiss-button>\n                <livelike-timer></livelike-timer>\n              </livelike-widget-header>\n              <livelike-widget-body>\n                <input\n                  type=\"number\"\n                  id=\"magnitude-input\"\n                  value=\"${this.initial_magnitude}\"\n                  min=\"0\" max=\"1\"\n                  style=\"width:50%\"\n                />\n                <button @click=${this.submitButtonClicked}>Submit Vote</button>\n                <livelike-select>\n                  <template>\n                    <livelike-option>\n                      <livelike-image height=\"60px\"></livelike-image>\n                    </livelike-option>\n                  </template>\n                </livelike-select>\n                <div>${this.average_magnitude}</div>\n              </livelike-widget-body>\n            </livelike-widget-root>\n          <template>\n        `;\n      }\n    }\n    customElements.define(\"custom-slider\", CustomSlider);",
      "language": "text"
    },
    {
      "code": "class CustomSlider extends LiveLikeEmojiSlider {\n  render() {\n    const initialMag = Math.round(this.widgetPayload.initial_magnitude * 100);\n    const resultMark =\n      this.phase !== 'interactive' && (this.val || this.val === 0)\n        ? html`\n            <div\n              class=\"result-mark\"\n              style=\"left: calc(${Math.round(\n                this.average_magnitude * 100\n              )}%)\"\n            ></div>\n          `\n        : null;\n\n    return html`\n      <template>\n        <style>\n\t\t\t\t\tlivelike-widget-root.custom-widget livelike-widget-header{\n            background: white;\n            text-align: center;\n            display: block;\n            padding-bottom: 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-bottom: 0;\n          }\n          livelike-widget-root.custom-widget livelike-timer.custom-timer{\n            background: #fac83c;\n            top: 0;\n            height: 5px;\n          }\n          livelike-widget-root.custom-widget .widget-kind{\n            color: #000;\n            opacity: 30%;\n            font-size: 14.5px;\n            letter-spacing: 0.55px;\n            font-family: \"HelveticaNeue-Medium\";\n            padding: 15px 20px 0 20px;\n          }\n          livelike-widget-root.custom-widget livelike-title.custom-title{\n            color: #000;\n            font-size: 20px;\n            font-family: \"HelveticaNeue-Bold\";\n            padding: 0 20px;\n            display: block;\n            width: calc(100% - 40px);\n          }\n          livelike-widget-root.custom-widget livelike-widget-body{\n            background: white;\n            padding: 0 20px 20px 20px;\n            border-radius: 0;\n            border: 1px solid #e6e6e6;\n            border-top: 0;\n          }\t\n          livelike-widget-root.custom-widget livelike-description{\n            font-size: 18.5px;\n            font-family: \"HelveticaNeue-Regular\";\n            text-align: left;\n          }\n          .slider-input::-webkit-slider-runnable-track {\n            height: 8px;\n            background: #e6e6e6;\n            background-image: linear-gradient(\n              90deg,\n              #140099,\n              #256eff var(--x),\n              transparent 0\n            );\n          }\n          .slider-input::-moz-range-track {\n            height: 8px;\n            background: #e6e6e6;\n            background-image: linear-gradient(\n              90deg,\n              #140099,\n              #256eff var(--x),\n              transparent 0\n            );\n          }\n          .slider-input::-ms-track {\n            height: 8px;\n            background: #e6e6e6;\n            background-image: linear-gradient(\n              90deg,\n              #140099,\n              #256eff var(--x),\n              transparent 0\n            );\n          }\n        </style>\n        <livelike-widget-root class=\"custom-widget\">\n          <livelike-widget-header class=\"widget-header\" slot=\"header\">\n            <livelike-timer class=\"custom-timer\"></livelike-timer>\n            <div class=\"widget-kind\">EMOJI SLIDER</div>\n            <livelike-title class=\"custom-title\"></livelike-title>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            <form style=\"--val: ${initialMag};\" class=\"input-form\">\n              <div class=\"input-container\">\n                <input\n                  type=\"range\"\n                  class=\"slider-input\"\n                  value=\"${initialMag}\"\n                />\n                ${resultMark}\n              </div>\n              <output class=\"slider-thumb\">\n                <img class=\"slider-image\" />\n              </output>\n            </form>\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-slider\", CustomSlider);\nconst widgetContainer = document.querySelector('livelike-widgets');\n\twidgetContainer.customWidgetRenderer = function({ widgetPayload }){\n  switch (widgetPayload.kind) {\n    case 'emoji-slider':\n      return document.createElement('custom-slider');\n    default:\n      break;\n  }\n};\n",
      "language": "javascript",
      "name": "Custom Slider Widget"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Text Ask Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "title",
    "1-0": "prompt",
    "2-0": "confirmation_message",
    "0-1": "String",
    "1-1": "String",
    "2-1": "String",
    "3-0": "submitReply",
    "3-1": "function: ()",
    "h-0": "Property",
    "h-1": "Type"
  },
  "cols": 2,
  "rows": 4
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomTextAsk extends LiveLikeTextAsk {\n  render() {\n    return html`\n      <template>\n        <livelike-widget-root>\n          <livelike-widget-header>\n            <livelike-title></livelike-title>\n            <livelike-timer></livelike-timer>\n            <livelike-dismiss-button></livelike-dismiss-button>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            <span>${this.prompt}</span>\n            <form>\n              <textarea\n                class=\"text-ask-input\"\n                type=\"text\"\n                name=\"reply\"\n                rows=\"2\"\n                .value = ${this.text}\n                maxlength=\"${this.maxlength}\"\n                ?disabled=\"${this.disabled}\"\n                placeholder=\"Type something...\"\n                @input=${this.inputHandler}\n              ></textarea>\n              ${ this.disabled ? null : html`<span class=\"text-ask-input-counter\">${this.maxlength}</span>` }\n            </form>\n            <button\n              @click=${this.submitReply}\n              ?disabled=\"${this.disabled || this.replyDisable}\"\n            >\n              <span>SEND</span>\n            </button>\n            <div class=\"${!this.showConfirmation ? 'hidden' : ''}\">\n              <span>${this.confirmation_message}</span>\n            </div>\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-text-ask\", CustomTextAsk);\n\nconst customWidgetRenderer = (args) => {\n  let widgetPayload = args.widgetPayload;\n  if( widgetPayload.kind === 'text-ask'){\n    return document.createElement('custom-text-ask');\n  }\n}\n\nlet w = document.querySelector('livelike-widgets');\nw.customWidgetRenderer = customWidgetRenderer;",
      "language": "text",
      "name": "Extend Text Ask Class"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Number Prediction Widget"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Type",
    "0-0": "question",
    "0-1": "String",
    "1-0": "options",
    "1-1": "Array",
    "2-0": "updateOption",
    "2-1": "function: (option, number: Integer)",
    "3-0": "lockInVote",
    "3-1": "function: (options: Array)"
  },
  "cols": 2,
  "rows": 4
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomImagePrediction extends LiveLikeNumberPrediction{\n  inputHandler = (e, option) => {\n    this.updateOption(option,+e.target.value);\n  }\n  render(){\n    return html `\n      <template>\n        <livelike-widget-root>\n          <livelike-widget-header slot=\"header\">\n            <livelike-title slot=\"title\"></livelike-title>\n            <livelike-dismiss-button slot=\"dismiss\"></livelike-dismiss-button>\n            <livelike-timer></livelike-timer>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            ${this.options.map((option,idx) => {\n              return html `\n              <livelike-option index=\"${idx}\">\n                <input \n                  type=\"number\" \n                  .value=\"${option.number}\"\n                  @input=${(e) => this.inputHandler(e,option)}\n                  ?disabled=\"${this.disabled || this.voteDisable}\"\n                />\n                <livelike-description></livelike-description>\n                <livelike-image height=\"80px\" width=\"80px\"></livelike-image>\n              </livelike-option>\n              `;\n            })}\n            <livelike-footer>\n              <button\n                @click=${() => this.lockInVote(this.options)}\n                ?disabled=\"${this.disabled || this.voteDisable || this.voteButtonDisabled}\"\n              >Vote</button>\n            </livelike-footer>\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-image-prediction\", CustomImagePrediction);\n\nconst customWidgetRenderer = (args) => {\n  let widgetPayload = args.widgetPayload;\n  if( widgetPayload.kind === 'image-number-prediction'){\n    return document.createElement('custom-image-prediction');\n  }\n}\n\nlet w = document.querySelector('livelike-widgets');\nw.customWidgetRenderer = customWidgetRenderer;",
      "language": "text",
      "name": "Image Number Prediction"
    },
    {
      "code": "class CustomImageFollowUp extends LiveLikeNumberFollowUp{\n  render(){\n    return html `\n      <template>\n        <livelike-widget-root>\n          <livelike-widget-header slot=\"header\">\n            <livelike-title slot=\"title\"></livelike-title>\n            <livelike-dismiss-button slot=\"dismiss\"></livelike-dismiss-button>\n            <livelike-timer></livelike-timer>\n          </livelike-widget-header>\n          <livelike-widget-body>\n            ${this.options.map((option,idx) => {\n              return html `\n              <livelike-option index=\"${idx}\">\n                <div>\n                  <span>User Input</span>\n                  <input \n                    type=\"number\" \n                    value=\"${option.number}\"\n                    disabled\n                  />\n                  <span>Correct Answer</span>\n                  <input \n                    type=\"number\" \n                    value=\"${option.correct_number}\"\n                    disabled\n                  />\n                </div>\n                <livelike-description></livelike-description>\n                <livelike-image height=\"80px\" width=\"80px\"></livelike-image>\n              </livelike-option>\n              `;\n            })}\n          </livelike-widget-body>\n        </livelike-widget-root>\n      </template>\n    `;\n  }\n}\ncustomElements.define(\"custom-image-followup\", CustomImageFollowUp);\n\nconst customWidgetRenderer = (args) => {\n  let widgetPayload = args.widgetPayload;\n  if(widgetPayload.kind === 'image-number-prediction-follow-up'){\n    return document.createElement('custom-image-followup');\n  }\n}\n\nlet w = document.querySelector('livelike-widgets');\nw.customWidgetRenderer = customWidgetRenderer;",
      "language": "text",
      "name": "Image Number Prediction Follow Up"
    }
  ]
}
[/block]