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

* *By extending widget classes*: This gives you full control over what you want to do with the widget, it is like creating a whole new widget using livelike widget as a base
* *By creating a custom template for a widget kind*: You define the template that gets returned from the livelike widget. You can add your own HTML tags in the template. Remove any component from the default widget template. We have various custom elements to help with the template building.

## Widget Classes

Widget classes can be extended to create any custom class which can be used to render widget instead of default widget. The available widget classes are:

* LiveLikePoll
* LiveLikeQuiz
* LiveLikePrediction
* LiveLikeFollowUp
* LiveLikeCheerMeter
* LiveLikeEmojiSlider
* LiveLikeRichPost
* LiveLikeSocialEmbed
* LiveLikeVideoAlert
* LiveLikeTextAsk
* LiveLikeNumberPrediction
* LiveLikeNumberFollowUp

## Custom Widget Rendering using classes

customElements can be defined from the classes created by extending livelike Widget Classes. These customElements can then be linked with the  livelike-widgets element using `customWidgetRenderer` method. The `customWidgetRenderer` method must return an HTMLTemplateElement, and the `widgetPayload` property is accessible as an argument

<Embed url="https://codepen.io/abhi1599/pen/wveNrdO" title="Custom Widget Rendering using classes" favicon="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" image="https://assets.codepen.io/6912090/internal/screenshots/pens/wveNrdO.default.png?fit=cover&amp;format=auto&amp;ha=false&amp;height=360&amp;quality=75&amp;v=2&amp;version=1632913139&amp;width=640" provider="codepen.io" href="https://codepen.io/abhi1599/pen/wveNrdO" html="%3Ciframe%20height%3D'350'%20scrolling%3D'no'%20src%3D'https%3A%2F%2Fcodepen.io%2Fabhi1599%2Fembed%2FwveNrdO'%20frameborder%3D'no'%20allowtransparency%3D'true'%20allowfullscreen%3D'true'%20style%3D'width%3A%20100%25%3B'%3E%3C%2Fiframe%3E" />

Remember not to use default livelike widget elements which are the following:

* livelike-text-poll
* livelike-image-poll
* livelike-text-quiz
* livelike-image-quiz
* livelike-text-prediction
* livelike-text-prediction-follow-up
* livelike-image-prediction
* livelike-image-prediction-follow-up
* livelike-cheer-meter
* livelike-emoji-slider
* livelike-rich-post
* livelike-social-embed
* livelike-video-alert
* livelike-text-ask
* livelike-text-number-prediction
* livelike-text-number-prediction-follow-up
* livelike-image-number-prediction
* livelike-image-number-prediction-follow-up

## Custom Widget Rendering using classes for different presentation modes

Different UI can be defined for each presentation mode by using the mode property of the \<livelike-widgets> element.

Here is an example with Number Prediction Widget custom UI only in interactive-timeline mode, for other modes stock UI is rendered by default.

<Embed url="https://codepen.io/abhi1599/pen/eYEKEpb" title="Custom Widget Rendering using classes for different presentation modes" favicon="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" provider="codepen.io" href="https://codepen.io/abhi1599/pen/eYEKEpb" html="%3Ciframe%20height%3D'350'%20scrolling%3D'no'%20src%3D'https%3A%2F%2Fcodepen.io%2Fabhi1599%2Fembed%2FeYEKEpb'%20frameborder%3D'no'%20allowtransparency%3D'true'%20allowfullscreen%3D'true'%20style%3D'width%3A%20100%25%3B'%3E%3C%2Fiframe%3E" />

## Widget Templates

Widgets can be customized by creating a template element with a `kind` attribute to declare what kind of widget will be rendered. The available widget kinds are:

* text-poll
* image-poll
* text-quiz
* image-quiz
* text-prediction
* text-prediction-follow-up
* image-prediction
* image-prediction-follow-up
* cheer-meter
* emoji-slider
* rich-post
* social-embed
* video-alert
* text-ask
* text-number-prediction
* text-number-prediction-follow-up
* image-number-prediction
* image-number-prediction-follow-up

The children of the template element will get rendered inside of the widget. 

```html Widget template
<!-- Template -->
<template kind="text-poll">
  <livelike-widget-root></livelike-widget-root>
</template>

<!-- What gets rendered -->
<livelike-text-poll>
  <livelike-widget-root></livelike-widget-root>
</livelike-text-poll>
```

Once a template is rendered on the page, all widgets of that same `kind` will be rendered using that template's children, whether the widget is getting rendered from a single tag on the page, or from being published from the CMS. 

If you require multiple different template's to be rendered conditionally per widget kind, read the `Custom Template Rendering` section below.

> 🚧 If using React, the template tag doesn't render in JSX the same way it does in HTML
>
> To write custom widget templates in JSX, one way would be to use the Higher Order Component below.
>
> For extending widget classes, customElements can be. created by extending widget classes as shown below and then the file in which customElements have been defined needs to be imported in the react component where \<livelike-widgets> is used

```javascript JSX Template
function Template({ children, ...attrs }) {
  return <template {...attrs} dangerouslySetInnerHTML={{ __html: children }} />;
}

<Template kind="text-poll">
  {`<livelike-widget-root></livelike-widget-root>`}
</Template>
```
```javascript Custom widget by extending class
import { html, LiveLikeAlert } from "@livelike/engagementsdk";

class CustomAlert extends LiveLikeAlert {
  render() {
    const hasCaptionAndMedia = !!this.text && !!this.image_url;

    const hasOnlyMedia = !this.text && !!this.image_url;

    const hasOnlyCaption = !!this.text && !this.image_url;

    const paramsString = !!this.link_url && new URLSearchParams(this.link_url.split('?')[1]);

    const hasSponsor = paramsString && paramsString.get("sponsor");

    return html`
      <template>
        <style>
          livelike-widget-root.custom-widget livelike-widget-header{
            background: white;
            text-align: center;
            display: block;
            padding-bottom: 20px;
            border-radius: 0;
            border: 1px solid #e6e6e6;
            border-bottom: 0;
          }
          livelike-widget-root.custom-widget livelike-timer.custom-timer{
            background: #fac83c;
            top: 0;
            height: 5px;
          }
          livelike-widget-root.custom-widget .widget-kind{
            color: #000;
            opacity: 30%;
            font-size: 14.5px;
            letter-spacing: 0.55px;
            font-family: "HelveticaNeue-Medium";
            padding: 15px 20px 0 20px;
          }
          livelike-widget-root.custom-widget livelike-title.custom-title{
            color: #000;
            font-size: 20px;
            font-family: "HelveticaNeue-Bold";
            padding: 0 20px;
            display: block;
            width: calc(100% - 40px);
          }
          livelike-widget-root.custom-widget livelike-widget-body{
            background: white;
            padding: 0 20px 20px 20px;
            border-radius: 0;
            border: 1px solid #e6e6e6;
            border-top: 0;
          }
          livelike-widget-root.custom-widget livelike-description{
            font-size: 18.5px;
            font-family: "HelveticaNeue-Regular";
            text-align: left;
          }
          livelike-footer a.widget-link{
            margin-top: 10px;
            border-radius: 5px;
            text-align: center;
            color: white;
            background-image: none;
            padding: 1rem;
            background-color: #222;
          }
          livelike-footer div.sponsor-section{
            margin-top: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
          }
          livelike-footer div.sponsor-section span{
            margin-right: 10px;
            color: #bbbbbb;
          }
          livelike-footer div.sponsor-section img{
            height: 30px;
            width: auto;
          }
          .widget-caption{
            color: #000;
            opacity: 60%;
          }
          .widget-media img{
            max-height: none;
            height: auto;
          }
        </style>
        <livelike-widget-root class="custom-widget">
          <livelike-widget-header class="widget-header" slot="header">
            <livelike-timer class="custom-timer"></livelike-timer>
            <div class="widget-kind">ALERT</div>
            <livelike-title class="custom-title"></livelike-title>
          </livelike-widget-header>
          <livelike-widget-body>
            ${hasCaptionAndMedia
              ? html`
                  <figure class="widget-captioned-media">
                    ${this.text &&
                      html`
                        <figcaption class="widget-caption media-caption">
                          ${this.text}
                        </figcaption>
                      `}
                    ${this.image_url &&
                      html`
                        <img
                          class="widget-media"
                          src=${this.image_url}
                          alt=${this.text}
                        />
                      `}
                  </figure>
                `
              : hasOnlyMedia
              ? html`
                  <div class="widget-media">
                    <img src=${this.image_url} />
                  </div>
                `
              : hasOnlyCaption
              ? html`
                  <div class="widget-caption-container">
                    <span class="widget-caption">${this.text}</span>
                  </div>
                `
              : null}
            ${this.link_url &&
              html`
                <livelike-footer>
                  <a
                    class="widget-link"
                    href=${this.link_url}
                    target="_blank"
                    @click=${this.trackLinkOpened}
                    >${this.link_label}</a>
                    ${hasSponsor &&
                      html`
                        <div class="sponsor-section">
                          <span>Sponsored by</span>
                          <img alt="sponsor logo" src="https://cf-blast-storage-qa.livelikecdn.com/assets/7eea3117-20ce-455e-8996-9021e62245b1.png"></img>
                        </div>
                    `}
                </livelike-footer>
              `}
          </livelike-widget-body>
        </livelike-widget-root>
      </template>
    `;
  }
}
customElements.define("custom-alert", CustomAlert);
```
```javascript React component using customElements
import "./custom-elements";
import { useEffect } from 'react';
import LiveLike from "@livelike/engagementsdk";

function App() {
  useEffect(() => {
    LiveLike.init({
        clientId: 'xxxxxxxxxxxxxxxxxx'
      }).then( p => {
        const widgetContainer = document.querySelector('livelike-widgets');
        widgetContainer.customWidgetRenderer = function({ widgetPayload }){
          switch (widgetPayload.kind) {
            case 'alert':
              return document.createElement('custom-alert');
            default:
              break;
          }
        };
      })
  },[]);
  return (
    <div className="App">
      <livelike-widgets programid="xxxxxxxxxxxx"></livelike-widgets>
    </div>
  );
}

export default App;
```

## Custom Template Rendering

Adding a template tag will render all widgets of that kind to have the markup of the template's children. To render different templates conditionally, the method `customTemplateRenderer` on the livelike-widgets element can be used. The `customTemplateRenderer` method must return an HTMLTemplateElement, and the `widgetPayload` property is accessible as an argument.  

```html
<livelike-widgets></livelike-widgets>
<template kind="alert" id="customAlert"></template>
<template kind="cheer-meter" id="customCheerMeter"></template>

<script>
const widgetContainer = document.querySelector('livelike-widgets');
widgetContainer.customTemplateRenderer = function({ widgetPayload }){
  switch (widgetPayload.kind) {
    case 'alert':
      return document.querySelector('template#customAlert');
    case 'cheer-meter':
      return document.querySelector('template#customCheerMeter');
      break;
    default:
      break;
  }
};
</script>
```

Properties from the `widgetPayload` can be used to create widgets in any way.

```html
<livelike-widgets></livelike-widgets>

<script>
const widgetContainer = document.querySelector('livelike-widgets');
                                               
function customImageAlert(widgetPayload){
  const alertWidget = document.createElement('template');
  alertWidget.innerHTML = `
    <h2>${widgetPayload.title}</h2>
    <img src="${widgetPayload.image_url}" />
		<span>${widgetPayload.text}</span>
  `;
  return alertWidget;
}

widgetContainer.customTemplateRenderer = function({ widgetPayload }){
	if(widgetPayload.kind === 'alert'){
    if(widgetPayload.image_url){
      return customImageAlert(widgetPayload);
    }
  }
};
</script>
```