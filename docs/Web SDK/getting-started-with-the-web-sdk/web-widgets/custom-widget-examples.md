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
## Alert Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Property
      </th>

      <th style={{ textAlign: "left" }}>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        title
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        text
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        image\_url
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        link\_url
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        link\_label
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        trackLinkOpened
      </td>

      <td style={{ textAlign: "left" }}>
        function: ()
      </td>
    </tr>
  </tbody>
</Table>

```javascript Alert Widget Example
const alertTemplate = (payload) => {
  var template = document.createElement('template');
  let alertHtml = `
    <livelike-widget-root>
      <livelike-widget-header>
        <livelike-title>${payload.title}</livelike-title>
      </livelike-widget-header>
      <livelike-widget-body>
        <img src=${payload.image_url}>
      	<a href="${payload.link_url}" target="_blank">${payload.link_label}</a>
      </livelike-widget-body>
    </livelike-widget-root>
  `;
  template.innerHTML = alertHtml;
  return template;
}
const widgetContainer = document.querySelector('livelike-widgets');
widgetContainer.customTemplateRenderer = function({ widgetPayload }){
  if(widgetPayload.kind === 'alert'){
    return alertTemplate(widgetPayload);
  }
}
```
```text Extended Alert Class
class CustomAlert extends LiveLikeAlert {
      render() {
        return html`
          <template>
            <livelike-widget-root>
              <livelike-widget-header>
              <livelike-title></livelike-title>
                ${this.link_url &&
                html`
                  <a href="${this.link_url}" target="_blank">${this.link_label}</a>
                `}
              </livelike-widget-header>
              <livelike-widget-body>
                <span>${this.text}</span>
                ${this.image_url &&
                html`
                  <img src=${this.image_url} height="40px">
                `}
              </livelike-widget-body>
            </livelike-widget-root>
          <template>
        `;
      }
    }
    customElements.define("custom-alert", CustomAlert);
    
const customWidgetRenderer = (args) => {
      let widgetPayload = args.widgetPayload;
      if( widgetPayload.kind === 'alert'){
        return document.createElement('custom-alert');
      }
    }
let w = document.querySelector('livelike-widgets');
w.customWidgetRenderer = customWidgetRenderer;
```
```javascript Custom Alert Widget
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
const widgetContainer = document.querySelector('livelike-widgets');
	widgetContainer.customWidgetRenderer = function({ widgetPayload }){
  switch (widgetPayload.kind) {
    case 'alert':
      return document.createElement('custom-alert');
    default:
      break;
  }
};
```

## Quiz Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        question
      </td>

      <td>
        question
      </td>
    </tr>

    <tr>
      <td>
        choices
      </td>

      <td>
        array
      </td>
    </tr>

    <tr>
      <td>
        lockInVote
      </td>

      <td>
        function: (option)
      </td>
    </tr>
  </tbody>
</Table>

```html Quiz Widget Example
<template kind="text-quiz">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
      <livelike-dismiss-button></livelike-dismiss-button>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
```
```html Custom Image Quiz
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
  livelike-widget-root.custom-widget livelike-select{
    background: #fff;
  }
  livelike-widget-root.custom-widget livelike-option{
    color: #000;
    border: 1px solid #e6e6e6;
    padding: 0;
    margin-bottom: 20px;
    height: auto;
  }
  livelike-widget-root.custom-widget livelike-option:last-child{
    margin-bottom: 0px;
  }
  livelike-widget-root.custom-widget livelike-option[selected]{
    color: #fff;
    background: #000;
  }
  livelike-widget-root.custom-widget livelike-description{
    font-size: 18.5px;
    font-family: "HelveticaNeue-Regular";
    text-align: left;
  }
  livelike-widget-root.custom-widget livelike-percentage{
    font-size: 21px;
    font-family: "HelveticaNeue-CondensedBlack"
  }
  livelike-widget-root.custom-widget livelike-progress{
    height: 4px;
    bottom: 0;
    top: auto;
    background: #e6e6e6;
    border-color: #e6e6e6;
    border-radius: 0;
  }
  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
    background: #0096ff;
    border-color: #0096ff;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 10px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{
    margin-bottom: 0;
    min-height: 60px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
    width: auto;
  }
  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{
    flex-grow: 1;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{
    background: #00ff78;
    border-color: #00ff78;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{
    background: #ff3c3c;
    border-color: #ff3c3c;
  }
</style>
<template kind="image-quiz">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">IMAGE QUIZ</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select class="image-grid">
        <template>
          <livelike-option>
            <div class="livelike-voting-image-container">
              <div class="image-description-wrapper">
                <livelike-description></livelike-description>
              </div>
              <livelike-percentage></livelike-percentage>
            </div>
            <livelike-image height="60px"></livelike-image>
            <livelike-progress></livelike-progress>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```

## Cheer Meter Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        title
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        options
      </td>

      <td>
        array
      </td>
    </tr>

    <tr>
      <td>
        submitVote
      </td>

      <td>
        function: (option)
      </td>
    </tr>
  </tbody>
</Table>

```html Cheer Meter Example
<template kind="cheer-meter">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-dismiss-button></livelike-dismiss-button>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select>
        <template>
          <livelike-option>
            <livelike-vote-count></livelike-vote-count>
            <livelike-description></livelike-description>
            <livelike-image height="50px" width="50px"></livelike-image>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```
```html Custom Cheer Meter
<script>
  class CustomCheerOption extends LiveLikeOption {
    votePercentage = () => {
      const totalVotes = this.items.reduce((a, b) => a + b['vote_count'], 0);
      return totalVotes > 0
        ? Math.round((this.item.vote_count / totalVotes) * 100)
        : 0;
    };
    render() {
      return html`
        <style>
          livelike-image{
            width: calc(100% - 42px);
            padding: 20px;
            border: 1px solid #e6e6e6;
            border-radius: 6px;
            flex-grow: 1;
          }
          :host(:not([disabled])) livelike-image:active{
            background-color: #222222 !important;
          }
          livelike-description{
            font-size: 18.5px;
            font-family: "HelveticaNeue-Regular";
            text-align: center;
            flex-grow: 0;
          }
        </style>
        <livelike-image width="100%" height="auto" style="background: linear-gradient(0deg, ${this.optionIndex % 2 === 0 ? `#0096ff` : `#ed174b` } ${this.votePercentage()}%, transparent 0);"></livelike-image>
        <livelike-description></livelike-description>
      `;
    }
}
customElements.define("custom-cheer-option", CustomCheerOption);
</script>
<style>
  body{
  background-color: #f0f0f0;
}
livelike-widgets{
  width: 500px;
  height: 340px;
  margin-left: auto;
  margin-right: auto;
}
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
livelike-widget-root.custom-widget livelike-select{
  background: #fff;
}
livelike-widget-root.custom-widget livelike-option{
  color: #000;
  border: 1px solid #e6e6e6;
  padding: 0;
  margin-bottom: 20px;
  height: auto;
}
livelike-widget-root.custom-widget livelike-option:last-child{
  margin-bottom: 0px;
}
livelike-widget-root.custom-widget livelike-option[selected]{
  color: #fff;
  background: #000;
}
livelike-widget-root.custom-widget livelike-description{
  font-size: 18.5px;
  font-family: "HelveticaNeue-Regular";
  text-align: left;
}
livelike-widget-root.custom-widget livelike-percentage{
  font-size: 21px;
  font-family: "HelveticaNeue-CondensedBlack"
}
livelike-widget-root.custom-widget livelike-progress{
  height: 4px;
  bottom: 0;
  top: auto;
  background: #e6e6e6;
  border-color: #e6e6e6;
  border-radius: 0;
}
livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
  background: #0096ff;
  border-color: #0096ff;
}
livelike-widget-root.custom-widget livelike-select.image-grid{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-column-gap: 15px;
  grid-row-gap: 10px;
}
livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{
  margin-bottom: 0;
  min-height: 60px;
}
livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
  width: auto;
}
livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{
  flex-grow: 1;
}
livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{
  background: #00ff78;
  border-color: #00ff78;
}
livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{
  background: #ff3c3c;
  border-color: #ff3c3c;
}
livelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid{
  width: 100%;
  background: transparent;
  display: flex;
  justify-content: space-around;
}
livelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid custom-cheer-option{
  display: flex;
  flex-direction: column;
  border: none;
  margin-bottom: 0;
  min-height: 60px;
  color: #000;
  padding: 0;
  height: auto;
  width: 100px;
}
livelike-cheer-meter livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
  width: calc(100% - 22px);
  padding: 10px;
  border: 1px solid #e6e6e6;
  border-radius: 6px;
}
livelike-cheer-meter livelike-widget-root.custom-widget img.divider{
  color: #000;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 2rem;
  z-index: 100;
}
livelike-cheer-meter livelike-widget-root.custom-widget livelike-description{
  text-align: center;
}
</style>
<template kind="cheer-meter">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">CHEER METER</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <div class="cheer-image-body">
        <livelike-vote-count></livelike-vote-count>
        <img class="divider" src="./assets/vs-light.gif" />
        <livelike-select class="image-grid">
          <template>
            <custom-cheer-option></custom-cheer-option>
          </template>
        </livelike-select>
      </div>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```

## Prediction Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        question
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        options
      </td>

      <td>
        array
      </td>
    </tr>

    <tr>
      <td>
        submitVote
      </td>

      <td>
        function: (option)
      </td>
    </tr>
  </tbody>
</Table>

```html Prediction widgets
<template kind="text-prediction">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
<template kind="image-prediction">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-image height="60px"></livelike-image>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
```
```html Follow-ups
<template kind="text-prediction-follow-up">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
<template kind="image-prediction-follow-up">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-image height="60px"></livelike-image>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
```
```html Custom Image Prediction
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
  livelike-widget-root.custom-widget livelike-select{
    background: #fff;
  }
  livelike-widget-root.custom-widget livelike-option{
    color: #000;
    border: 1px solid #e6e6e6;
    padding: 0;
    margin-bottom: 20px;
    height: auto;
  }
  livelike-widget-root.custom-widget livelike-option:last-child{
    margin-bottom: 0px;
  }
  livelike-widget-root.custom-widget livelike-option[selected]{
    color: #fff;
    background: #000;
  }
  livelike-widget-root.custom-widget livelike-description{
    font-size: 18.5px;
    font-family: "HelveticaNeue-Regular";
    text-align: left;
  }
  livelike-widget-root.custom-widget livelike-percentage{
    font-size: 21px;
    font-family: "HelveticaNeue-CondensedBlack"
  }
  livelike-widget-root.custom-widget livelike-progress{
    height: 4px;
    bottom: 0;
    top: auto;
    background: #e6e6e6;
    border-color: #e6e6e6;
    border-radius: 0;
  }
  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
    background: #0096ff;
    border-color: #0096ff;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 10px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{
    margin-bottom: 0;
    min-height: 60px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
    width: auto;
  }
  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{
    flex-grow: 1;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{
    background: #00ff78;
    border-color: #00ff78;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{
    background: #ff3c3c;
    border-color: #ff3c3c;
  }
</style>
<template kind="image-prediction">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">IMAGE PREDICTION</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select class="image-grid prediction-widget">
        <template>
          <livelike-option>
            <div class="livelike-voting-image-container">
              <div class="image-description-wrapper">
                <livelike-description></livelike-description>
              </div>
              <livelike-percentage></livelike-percentage>
            </div>
            <livelike-image height="60px"></livelike-image>
            <livelike-progress></livelike-progress>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```
```html Custom Image Prediction Follow Up
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
  livelike-widget-root.custom-widget livelike-select{
    background: #fff;
  }
  livelike-widget-root.custom-widget livelike-option{
    color: #000;
    border: 1px solid #e6e6e6;
    padding: 0;
    margin-bottom: 20px;
    height: auto;
  }
  livelike-widget-root.custom-widget livelike-option:last-child{
    margin-bottom: 0px;
  }
  livelike-widget-root.custom-widget livelike-option[selected]{
    color: #fff;
    background: #000;
  }
  livelike-widget-root.custom-widget livelike-description{
    font-size: 18.5px;
    font-family: "HelveticaNeue-Regular";
    text-align: left;
  }
  livelike-widget-root.custom-widget livelike-percentage{
    font-size: 21px;
    font-family: "HelveticaNeue-CondensedBlack"
  }
  livelike-widget-root.custom-widget livelike-progress{
    height: 4px;
    bottom: 0;
    top: auto;
    background: #e6e6e6;
    border-color: #e6e6e6;
    border-radius: 0;
  }
  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
    background: #0096ff;
    border-color: #0096ff;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 10px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{
    margin-bottom: 0;
    min-height: 60px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
    width: auto;
  }
  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{
    flex-grow: 1;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{
    background: #00ff78;
    border-color: #00ff78;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{
    background: #ff3c3c;
    border-color: #ff3c3c;
  }
</style>
<template kind="image-prediction-follow-up">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">IMAGE PREDICTION FOLLOW UP</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select class="image-grid">
        <template>
          <livelike-option>
            <div class="livelike-voting-image-container">
              <div class="image-description-wrapper">
                <livelike-description></livelike-description>
              </div>
              <livelike-percentage></livelike-percentage>
            </div>
            <livelike-image height="60px"></livelike-image>
            <livelike-progress></livelike-progress>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```

## Poll Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        question
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        options
      </td>

      <td>
        array
      </td>
    </tr>

    <tr>
      <td>
        submitVote
      </td>

      <td>
        function: (option)
      </td>
    </tr>
  </tbody>
</Table>

```text
<template kind="text-poll">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
<template kind="image-poll">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
    </livelike-widget-header>
    <livelike-select>
      <template>
        <livelike-option>
          <livelike-image height="60px"></livelike-image>
          <livelike-description></livelike-description>
          <livelike-percentage></livelike-percentage>
          <livelike-vote-count></livelike-vote-count>
        </livelike-option>
      </template>
    </livelike-select>
  </livelike-widget-root>
</template>
```
```html Customized Text Poll
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
  livelike-widget-root.custom-widget livelike-select{
    background: #fff;
  }
  livelike-widget-root.custom-widget livelike-option{
    color: #000;
    border: 1px solid #e6e6e6;
    padding: 0;
    margin-bottom: 20px;
    height: auto;
  }
  livelike-widget-root.custom-widget livelike-option:last-child{
    margin-bottom: 0px;
  }
  livelike-widget-root.custom-widget livelike-option[selected]{
    color: #fff;
    background: #000;
  }
  livelike-widget-root.custom-widget livelike-description{
    font-size: 18.5px;
    font-family: "HelveticaNeue-Regular";
    text-align: left;
  }
  livelike-widget-root.custom-widget livelike-percentage{
    font-size: 21px;
    font-family: "HelveticaNeue-CondensedBlack"
  }
  livelike-widget-root.custom-widget livelike-progress{
    height: 4px;
    bottom: 0;
    top: auto;
    background: #e6e6e6;
    border-color: #e6e6e6;
    border-radius: 0;
  }
  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
    background: #0096ff;
    border-color: #0096ff;
  }
</style>
<template kind="text-poll">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">TEXT POLL</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select>
        <template>
          <livelike-option>
            <div style="width:100%;display:flex;align-items:center;">
              <livelike-progress></livelike-progress>
              <livelike-description></livelike-description>
              <livelike-percentage></livelike-percentage>
            </div>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```
```html Customized Image Poll
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
  livelike-widget-root.custom-widget livelike-select{
    background: #fff;
  }
  livelike-widget-root.custom-widget livelike-option{
    color: #000;
    border: 1px solid #e6e6e6;
    padding: 0;
    margin-bottom: 20px;
    height: auto;
  }
  livelike-widget-root.custom-widget livelike-option:last-child{
    margin-bottom: 0px;
  }
  livelike-widget-root.custom-widget livelike-option[selected]{
    color: #fff;
    background: #000;
  }
  livelike-widget-root.custom-widget livelike-description{
    font-size: 18.5px;
    font-family: "HelveticaNeue-Regular";
    text-align: left;
  }
  livelike-widget-root.custom-widget livelike-percentage{
    font-size: 21px;
    font-family: "HelveticaNeue-CondensedBlack"
  }
  livelike-widget-root.custom-widget livelike-progress{
    height: 4px;
    bottom: 0;
    top: auto;
    background: #e6e6e6;
    border-color: #e6e6e6;
    border-radius: 0;
  }
  livelike-widget-root.custom-widget livelike-option[selected] livelike-progress{
    background: #0096ff;
    border-color: #0096ff;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 10px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-option{
    margin-bottom: 0;
    min-height: 60px;
  }
  livelike-widget-root.custom-widget livelike-select.image-grid livelike-image{
    width: auto;
  }
  livelike-widget-root.custom-widget livelike-option div.livelike-voting-image-container{
    flex-grow: 1;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[correct] livelike-progress{
    background: #00ff78;
    border-color: #00ff78;
  }
  livelike-widget-root.custom-widget livelike-select:not(.prediction-widget) livelike-option[incorrect] livelike-progress{
    background: #ff3c3c;
    border-color: #ff3c3c;
  }
</style>
<template kind="image-poll">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header class="widget-header" slot="header">
      <livelike-timer class="custom-timer"></livelike-timer>
      <div class="widget-kind">IMAGE POLL</div>
      <livelike-title class="custom-title"></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select class="image-grid">
        <template>
          <livelike-option>
            <div class="livelike-voting-image-container">
              <div class="image-description-wrapper">
                <livelike-description></livelike-description>
              </div>
              <livelike-percentage></livelike-percentage>
            </div>
            <livelike-image height="60px"></livelike-image>
            <livelike-progress></livelike-progress>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```

## Slider Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        question
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        options
      </td>

      <td>
        array
      </td>
    </tr>

    <tr>
      <td>
        average\_magnitude
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        initial\_magnitude
      </td>

      <td>
        string
      </td>
    </tr>

    <tr>
      <td>
        lockInVote
      </td>

      <td>
        function: (magnitude: number)
      </td>
    </tr>
  </tbody>
</Table>

```text
class CustomSlider extends LiveLikeEmojiSlider {
      submitButtonClicked = () => {
        let mag = this.querySelector('#magnitude-input').value;
        this.submitResults(mag).then((r) => console.log('slider vote submitted', r));
      }
      render() {
        return html`
          <template>
            <livelike-widget-root>
              <livelike-widget-header>
                <livelike-title slot="title"></livelike-title>
                <livelike-dismiss-button slot="dismiss"></livelike-dismiss-button>
                <livelike-timer></livelike-timer>
              </livelike-widget-header>
              <livelike-widget-body>
                <input
                  type="number"
                  id="magnitude-input"
                  value="${this.initial_magnitude}"
                  min="0" max="1"
                  style="width:50%"
                />
                <button @click=${this.submitButtonClicked}>Submit Vote</button>
                <livelike-select>
                  <template>
                    <livelike-option>
                      <livelike-image height="60px"></livelike-image>
                    </livelike-option>
                  </template>
                </livelike-select>
                <div>${this.average_magnitude}</div>
              </livelike-widget-body>
            </livelike-widget-root>
          <template>
        `;
      }
    }
    customElements.define("custom-slider", CustomSlider);
```
```javascript Custom Slider Widget
class CustomSlider extends LiveLikeEmojiSlider {
  render() {
    const initialMag = Math.round(this.widgetPayload.initial_magnitude * 100);
    const resultMark =
      this.phase !== 'interactive' && (this.val || this.val === 0)
        ? html`
            <div
              class="result-mark"
              style="left: calc(${Math.round(
                this.average_magnitude * 100
              )}%)"
            ></div>
          `
        : null;

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
          .slider-input::-webkit-slider-runnable-track {
            height: 8px;
            background: #e6e6e6;
            background-image: linear-gradient(
              90deg,
              #140099,
              #256eff var(--x),
              transparent 0
            );
          }
          .slider-input::-moz-range-track {
            height: 8px;
            background: #e6e6e6;
            background-image: linear-gradient(
              90deg,
              #140099,
              #256eff var(--x),
              transparent 0
            );
          }
          .slider-input::-ms-track {
            height: 8px;
            background: #e6e6e6;
            background-image: linear-gradient(
              90deg,
              #140099,
              #256eff var(--x),
              transparent 0
            );
          }
        </style>
        <livelike-widget-root class="custom-widget">
          <livelike-widget-header class="widget-header" slot="header">
            <livelike-timer class="custom-timer"></livelike-timer>
            <div class="widget-kind">EMOJI SLIDER</div>
            <livelike-title class="custom-title"></livelike-title>
          </livelike-widget-header>
          <livelike-widget-body>
            <form style="--val: ${initialMag};" class="input-form">
              <div class="input-container">
                <input
                  type="range"
                  class="slider-input"
                  value="${initialMag}"
                />
                ${resultMark}
              </div>
              <output class="slider-thumb">
                <img class="slider-image" />
              </output>
            </form>
          </livelike-widget-body>
        </livelike-widget-root>
      </template>
    `;
  }
}
customElements.define("custom-slider", CustomSlider);
const widgetContainer = document.querySelector('livelike-widgets');
	widgetContainer.customWidgetRenderer = function({ widgetPayload }){
  switch (widgetPayload.kind) {
    case 'emoji-slider':
      return document.createElement('custom-slider');
    default:
      break;
  }
};
```

## Text Ask Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        title
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        prompt
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        confirmation\_message
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        submitReply
      </td>

      <td>
        function: ()
      </td>
    </tr>
  </tbody>
</Table>

```text Extend Text Ask Class
class CustomTextAsk extends LiveLikeTextAsk {
  render() {
    return html`
      <template>
        <livelike-widget-root>
          <livelike-widget-header>
            <livelike-title></livelike-title>
            <livelike-timer></livelike-timer>
            <livelike-dismiss-button></livelike-dismiss-button>
          </livelike-widget-header>
          <livelike-widget-body>
            <span>${this.prompt}</span>
            <form>
              <textarea
                class="text-ask-input"
                type="text"
                name="reply"
                rows="2"
                .value = ${this.text}
                maxlength="${this.maxlength}"
                ?disabled="${this.disabled}"
                placeholder="Type something..."
                @input=${this.inputHandler}
              ></textarea>
              ${ this.disabled ? null : html`<span class="text-ask-input-counter">${this.maxlength}</span>` }
            </form>
            <button
              @click=${this.submitReply}
              ?disabled="${this.disabled || this.replyDisable}"
            >
              <span>SEND</span>
            </button>
            <div class="${!this.showConfirmation ? 'hidden' : ''}">
              <span>${this.confirmation_message}</span>
            </div>
          </livelike-widget-body>
        </livelike-widget-root>
      </template>
    `;
  }
}
customElements.define("custom-text-ask", CustomTextAsk);

const customWidgetRenderer = (args) => {
  let widgetPayload = args.widgetPayload;
  if( widgetPayload.kind === 'text-ask'){
    return document.createElement('custom-text-ask');
  }
}

let w = document.querySelector('livelike-widgets');
w.customWidgetRenderer = customWidgetRenderer;
```

## Number Prediction Widget

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property
      </th>

      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        question
      </td>

      <td>
        String
      </td>
    </tr>

    <tr>
      <td>
        options
      </td>

      <td>
        Array
      </td>
    </tr>

    <tr>
      <td>
        updateOption
      </td>

      <td>
        function: (option, number: Integer)
      </td>
    </tr>

    <tr>
      <td>
        lockInVote
      </td>

      <td>
        function: (options: Array)
      </td>
    </tr>
  </tbody>
</Table>

```text Image Number Prediction
class CustomImagePrediction extends LiveLikeNumberPrediction{
  inputHandler = (e, option) => {
    this.updateOption(option,+e.target.value);
  }
  render(){
    return html `
      <template>
        <livelike-widget-root>
          <livelike-widget-header slot="header">
            <livelike-title slot="title"></livelike-title>
            <livelike-dismiss-button slot="dismiss"></livelike-dismiss-button>
            <livelike-timer></livelike-timer>
          </livelike-widget-header>
          <livelike-widget-body>
            ${this.options.map((option,idx) => {
              return html `
              <livelike-option index="${idx}">
                <input 
                  type="number" 
                  .value="${option.number}"
                  @input=${(e) => this.inputHandler(e,option)}
                  ?disabled="${this.disabled || this.voteDisable}"
                />
                <livelike-description></livelike-description>
                <livelike-image height="80px" width="80px"></livelike-image>
              </livelike-option>
              `;
            })}
            <livelike-footer>
              <button
                @click=${() => this.lockInVote(this.options)}
                ?disabled="${this.disabled || this.voteDisable || this.voteButtonDisabled}"
              >Vote</button>
            </livelike-footer>
          </livelike-widget-body>
        </livelike-widget-root>
      </template>
    `;
  }
}
customElements.define("custom-image-prediction", CustomImagePrediction);

const customWidgetRenderer = (args) => {
  let widgetPayload = args.widgetPayload;
  if( widgetPayload.kind === 'image-number-prediction'){
    return document.createElement('custom-image-prediction');
  }
}

let w = document.querySelector('livelike-widgets');
w.customWidgetRenderer = customWidgetRenderer;
```
```text Image Number Prediction Follow Up
class CustomImageFollowUp extends LiveLikeNumberFollowUp{
  render(){
    return html `
      <template>
        <livelike-widget-root>
          <livelike-widget-header slot="header">
            <livelike-title slot="title"></livelike-title>
            <livelike-dismiss-button slot="dismiss"></livelike-dismiss-button>
            <livelike-timer></livelike-timer>
          </livelike-widget-header>
          <livelike-widget-body>
            ${this.options.map((option,idx) => {
              return html `
              <livelike-option index="${idx}">
                <div>
                  <span>User Input</span>
                  <input 
                    type="number" 
                    value="${option.number}"
                    disabled
                  />
                  <span>Correct Answer</span>
                  <input 
                    type="number" 
                    value="${option.correct_number}"
                    disabled
                  />
                </div>
                <livelike-description></livelike-description>
                <livelike-image height="80px" width="80px"></livelike-image>
              </livelike-option>
              `;
            })}
          </livelike-widget-body>
        </livelike-widget-root>
      </template>
    `;
  }
}
customElements.define("custom-image-followup", CustomImageFollowUp);

const customWidgetRenderer = (args) => {
  let widgetPayload = args.widgetPayload;
  if(widgetPayload.kind === 'image-number-prediction-follow-up'){
    return document.createElement('custom-image-followup');
  }
}

let w = document.querySelector('livelike-widgets');
w.customWidgetRenderer = customWidgetRenderer;
```
