---
title: Customize Comments Web UI
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
### c. Customise UI component

When it comes to customising the UI components within LiveLikeComments, you have the flexibility to adapt it to your unique needs. To achieve this, follow these steps:

1. Extend the LiveLikeComments Component: Begin by extending the LiveLikeComments Web component class in your project. This will allow you to have full control over the methods inside the component.
2. Within your extended class, you can customise various parts of the UI based on your specific requirements.

#### Customise the Header UI :

Here's an example of how you can customise the comment board header component.

```javascript
import { LiveLikeComments, html } from "@livelike/engagementsdk";

class CustomLiveLikeCommentHeader extends LiveLikeComments {
    renderCommentBoardHeader() {
        return html`
            <div class="comment-board-header">
                <div class="avatar">
                    <img src="avatar.jpg" alt="User Avatar">
                </div>
                <h1>Custom comment board Title</h1>
                <div class="subtitle">Share your thoughts and opinions</div>
                <div class="comment-count">${this.commentTotalCount} Comments</div>
            </div>
        `;
    }
}

if (!customElements.get("livelike-comment-board-header")) {
    customElements.define("livelike-comment-board-header", CustomLiveLikeCommentHeader);
}

```