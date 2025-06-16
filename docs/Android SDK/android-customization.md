---
title: Custom Theming
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Theming | Android SDK | LiveLike
  description: >-
    The Android Engagement SDK allows you to customize a variety of visual
    attributes on the widget and chat elements.
  robots: index
next:
  description: ''
---
The Engagement SDK allows you to customize a variety of visual attributes on the widget and chat elements in order to achieve your desired visual themes.
[block:api-header]
{
  "title": "Widget Theming"
}
[/block]
You can theme widgets in a variety of different ways as shown below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif",
        "Screen Recording 2019-09-16 at 04.23 PM.gif",
        729,
        145,
        "#a093a4"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif",
        "Screen Recording 2019-09-16 at 04.24 PM.gif",
        726,
        149,
        "#cbc0c3"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif",
        "Screen Recording 2019-09-16 at 04.24 PM (1).gif",
        725,
        146,
        "#7591ac"
      ]
    }
  ]
}
[/block]
On Android, you can override the default values of colors, fonts, and dimensions in the values folder of the SDK. The customizable variables and their functions are listed below:

### Colors

You can override the color values by setting your own. The default values for the SDK are listed in the **colors.xml** resource file.
[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n  <summary>Common</summary>\n  <br>\n  <p><code>livelike_default_text_color</code> : Default color for all text in the SDK.</p>\n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Widget Headers</summary>\n<br>\n<p>These control the gradient colors of the title. You can set them to be the same to get a single solid color title background.</p>\n<br>\n  <p><code>livelike_header_text_color</code> : The color of the title text in a widget, same as default text color</p>\n  <br>\n  <p>Poll View</p>\n  <ul>\n    <li>* <code>livelike_poll_title_gradient_left</code> </li>\n    <li>* <code>livelike_poll_title_gradient_right</code> </li>\n  </ul>  \n<br>\n  <p>Quiz View</p>\n  <ul>\n  <li>* <code>livelike_quiz_title_gradient_left</code> </li>\n  <li>* <code>livelike_quiz_title_gradient_right</code> </li>\n  </ul>\n  <br>\n  <p>Prediction View</p>\n  <ul>\n    <li>* <code>livelike_prediction_title_gradient_left</code> </li>\n    <li>* <code>livelike_prediction_title_gradient_right</code> </li>\n  <ul>\n<br>\n    <p>Emoji Slider</p>\n    <ul>\n      <li>* <code>livelike_image_slider_header_bg</code></li>\n    </ul>   \n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n<details>\n<summary>Widget Options</summary>\n<br>\n<p>Poll Option: These are the colors of percentage bar and border for the poll option view.</p>\n<ul>\n  <li>* <code>livelike_poll_bar_gradient_left</code></li>\n  <li>* <code>livelike_poll_bar_gradient_right</code></li>\n  <li>* <code>livelike_poll_option_selected_border</code></li>\n</ul>\n<br>\n  <p>Quiz Option: These are the colors of percentage bar and border for the quiz option view.</p>\n  <ul>\n    <li>* <code>livelike_quiz_bar_gradient_left</code></li>\n    <li>* <code>livelike_quiz_bar_gradient_right</code></li>\n    <li>* <code>livelike_quiz_option_selected_border</code></li>\n  </ul> \n<br>\n  <p>Prediction Option: These are the colors of percentage bar and border for the prediction option view.</p>\n  <ul>\n    <li>* <code>livelike_prediction_option_selected_border</code></li>\n    <li>* <code>livelike_prediction_image_option_selected_border</code></li>\n  </ul>  \n  <br>\n  <p>Not Selected option: These are the colors of percentage bar for the not selected option view for all options.</p>\n<ul>\n  <li>* <code>livelike_neutral_bar_gradient_left</code></li>\n  <li>* <code>livelike_neutral_bar_gradient_right</code></li>\n</ul>  \n<br>\n<p>Text Color:</p>\n<ul>\n  <li>* <code>livelike_option_text_color</code> : Default text color in the options, same as default text color.</li>\n</ul>\n<br>\n<p>Right and wrong answer percentage bar : For widgets where the percentage bar's and border color is different based on user input:</p>\n<ul>\n  <li>* <code>livelike_correct_bar_gradient_left</code></li>\n  <li>* <code>livelike_correct_bar_gradient_right</code></li>\n  <li>* <code>livelike_incorrect_bar_gradient_left</code></li>\n  <li>* <code>livelike_incorrect_bar_gradient_right</code></li>\n  <li>* <code>livelike_neutral_bar_gradient_left</code></li>\n  <li>* <code>livelike_neutral_bar_gradient_right</code></li>\n  <li>* <code>livelike_correct_option_border_color</code></li>\n  <li>* <code>livelike_incorrect_option_border_color</code></li>\n</ul>\n <br>\n  <p> Option Background: For updating the background color of every option(not the progress color)</p> \n  <ul>\n  <li><code>livelike_default_button_background_color</code></li>\n  </ul> \n <br>\n  <p>Emoji Slider: For updating the style of emoji slider</p>\n  <ul>\n    <li>* <code>livelike_image_slider_gradient_start</code></li>\n    <li>* <code>livelike_image_slider_gradient_end</code></li>\n    <li>* <code>livelike_image_slider_bg</code></li>\n    <li>* <code>livelike_image_slider_widget_result_end_color</code></li>\n    <li>* <code>livelike_image_slider_widget_result_center_color</code></li>\n  </ul>  \n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Alert Widget</summary>\n<br>\n<p><strong>Header</strong><p>\n  <p>The title bar's background color gradients:</p>\n  <ul>\n    <li>* <code>livelike_alert_notification_label_gradient_left</code></li>\n    <li>* <code>livelike_alert_notification_label_gradient_right</code></li>\n    <li>* <code>livelike_alert_label_background_shadow</code> : Shadow color of the title</li>\n    <br>\n    <p> To have custom background with customize drawable ,create a drawable with name <code>alert_notification_label_background.xml</code> ,this will override the current header background with your drawable.</p>\n  </ul>\n  <br>\n  <p><strong>Body</strong></p>\n  <p>Background Color:</p>\n  <ul>\n    <li>* <code>livelike_alert_background_gradient_left</code></li>\n    <li>* <code>livelike_alert_background_gradient_right</code></li>\n    <br>\n    <p>Text Color:</p>\n    <li>* <code>livelike_alert_body_text_color</code> : The color of the body text of the alert</li>\n    <li>* <code>livelike_alert_link_text_color</code> : Color of the link text</li>\n    <li>* <code>livelike_alert_label_text_color</code> : Color of the header text</li>\n  </ul>\n  </details>\n\n<br>"
}
[/block]
### Fonts

Font size can be controlled via the variables listed in **dimens.xml**.
[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Common</summary>\n<br>\n<ul>\n  <li>* <code>livelike_header_text_size</code> : The font size of the header text.</li>\n  <li>* <code>livelike_option_text_size</code> : The font size of the options text.</li>\n  <li>* <code>livelike_percent_label_text_size</code> : The percentage bar text size.</li>\n</ul>\n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Alert Widget</summary>\n<br>\n<ul>\n  <li>* <code>livelike_alert_body_text_size</code> : Alert widget body text size.</li>\n  <li>* <code>livelike_alert_link_text_size</code> : Alert link text size.</li>\n  <li>* <code>livelike_alert_label_text_size</code> : Alert label text size.</li>\n</ul>\n</details>\n\n<br>"
}
[/block]

### Other

These include variables like border radius and stroke width of most ui elements.
[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Details</summary>\n<br>\n<ul>\n  <li>* <code>livelike_percent_bar_corner_radius</code></li>\n  <li>* <code>livelike_percent_bar_corner_radius_image</code></li>\n  <li>* <code>livelike_header_corner_radius</code></li>\n  <li>* <code>livelike_header_background_notification_label_radius</code></li>\n  <li>* <code>livelike_chat_rounded_rect_radius</code></li>\n  <li>* <code>livelike_button_corner_radius</code></li>\n  <li>* <code>livelike_button_outline_stroke_width</code></li>\n  <li>* <code>livelike_confirm_outline_stroke_width</code></li>\n  <li>* <code>livelike_header_outline_stroke_width</code></li>\n</ul>\n</details>\n\n<br>"
}
[/block]

[block:api-header]
{
  "title": "Chat Theming"
}
[/block]
Just like the widgets, the chat component is also customizable through overriding the default values provided in the dimens/colors/attrs xml files with values in XML files in the integrating application. The variables available for customization are listed below:
[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Chat View</summary>\n<br>\n<p>The chat view is designed to fill the parent view. So its height and width can be controlled directly by the integrator by controlling the height and width of the view provided by them.</p>\n<p><strong>Background</strong></p>\n<p>Gradient start and end color:</p>\n<ul>\n  <li>* <code>livelike_chat_background_end_color</code>, color</li>\n  <li>* <code>livelike_chat_background_start_color</code>, color</li>\n</ul>\n<br>\n<p>Gradient angle:</p>\n<ul>\n  <li>* <code>livelike_chat_background_gradient_angle</code>, integer</li>\n</ul>\n<br>\n<p><strong>Username</strong></p>\n<p>Default color of the text:</p>\n<ul>\n  <li>* <code>livelike_openChatNicknameOther</code>, color</li>\n</ul>\n<br>\n<p>Color of the text if message sent by current user:</p>\n<ul>\n  <li>* <code>livelike_openChatNicknameMe</code>, color</li>\n</ul>\n<br>\n<p>Font size of the text:</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_name_size</code>, dimen</li>\n</ul>\n<br>\n<p><strong>Message</strong></p>\n<p>Text color:</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_message_color</code>, color</li>\n</ul><br>\n<p>Text font size:</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_text_size</code>, dimen</li>\n</ul><br>\n<p><strong>Chat Bubble</strong></p>\n<p>Border radius of chat bubble:</p>\n<ul>\n  <li>* <code>livelike_chat_rounded_rect_radius</code>, dimen</li>\n</ul><br>\n<p>Background color of the chat message:</p>\n<ul>\n  <li>* <code>livelike_chat_rounded_rect_color</code>, color</li>\n</ul><br>\n<p>Padding (Horizontal/Vertical):</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_padding_horizontal</code>, dimen</li><br>\n  <li>* <code>livelike_default_chat_cell_padding_vertical</code>, dimen</li>\n</ul><br>\n<p>Padding (Each Side):</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_padding_left</code>, dimen</li>\n  <li>* <code>livelike_default_chat_cell_padding_right</code>, dimen</li>\n  <li>* <code>livelike_default_chat_cell_padding_top</code>, dimen</li>\n  <li>* <code>livelike_default_chat_cell_padding_bottom</code>, dimen</li>\n</ul><br>\n<p>Margin:</p>\n<ul>\n  <li>* <code>livelike_default_chat_cell_margin_vertical</code>, dimen</li>\n</ul><br>\n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Chat Input</summary>\n<br>\n<ul>\n<li>* Font size: <code>livelike_default_chat_input_text_size</code>, dimen</li>\n\n<li>* Font color: <code>livelike_chat_input_text_color</code>, color</li>\n\n<li>* Background Color: <code>livelike_chat_input_background_color</code>, color</li>\n\n<li>* Border Radius: <code>livelike_default_chat_input_border_radius</code>, dimen</li>\n\n<li>* Border Color: <code>livelike_chat_input_border_color</code>, color</li>\n\n<li>* Border Width: <code>livelike_default_chat_input_border_stroke</code>, dimen</li>\n\n<li>* Margin: <code>livelike_default_chat_input_margin_bottom</code>, dimen</li>\n</ul>\n</details>"
}
[/block]

[block:html]
{
  "html": "<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->\n\n<details>\n<summary>Snap To Live</summary>\n<br>\n<ul>\n<li>Background color: <code>livelike_live_button_background_color</code>, color</li>\n\n<li>Arrow color: <code>livelike_live_button_arrow_color</code>, color</li>\n</ul>\n</details>\n\n<br>"
}
[/block]
**Advanced Chat Customization**

As an integrator, you are able to customize the look and feel of the experience you provide to your users through the XML custom attributes using in layout. Create the theme and add the attributes you want to update.
[block:code]
{
  "codes": [
    {
      "code": "<style name=\"CustomChatTheme\" parent=\"AppTheme\">\n        <item name=\"displayUserProfile\">false</item><!-- To display the gamification display in chatView -->\n        <item name=\"chatWidth\">match_parent</item><!-- to update the width od chat bubble -->\n        <item name=\"chatBubbleBackground\">#FFF</item><!-- to update the background of chat bubble,it can be drawable/color -->\n        <item name=\"chatBackground\">#FFF</item><!-- update the background of chat message box,it can be drawable/color -->\n        <item name=\"usernameColor\">#000</item><!-- update the color of username in chat message -->\n        <item name=\"otherUsernameColor\">#000</item><!-- update the color of different username in chat message -->\n        <item name=\"messageColor\">#5f5f5f</item><!-- update color of message in chat message -->\n        <item name=\"chatInputViewBackground\">#FFF</item><!-- update the background of ChatInput, it can be drawable/color -->\n        <item name=\"chatDisplayBackground\">#efeff4</item><!-- update the background of Chat List, it can be drawable/color  -->\n        <item name=\"chatViewBackground\">#FFF</item><!-- update the background of full ChatFull View, it can be drawable/color --> \n        <item name=\"chatInputTextColor\">#8e8e93</item><!-- update the color of textInput -->\n        <item name=\"chatInputTextSize\">15sp</item><!-- update the textsize of textInput -->\n        <item name=\"chatInputTextHintColor\">#8e8e93</item><!-- update the hint color of textInput -->\n  <!--update the margin for chat box -->\n        <item name=\"chatMarginBottom\">3dp</item>\n        <item name=\"chatMarginTop\">0dp</item>\n        <item name=\"chatMarginLeft\">0dp</item>\n        <item name=\"chatMarginRight\">0dp</item>\n  <!--update the margin for chat box -->\n  <!-- update the position of ChatReactionView -->\n        <item name=\"chatReactionXPosition\">120dp</item>\n        <item name=\"chatReactionYPosition\">25dp</item>\n  <!-- update the position of ChatReactionView -->\n        <item name=\"chatReactionElevation\">6dp</item><!-- update the elevation of chat reaction (CardView) -->\n        <item name=\"chatReactionRadius\">20dp</item> <!-- update the chat Reaction(CardView) View corner radius -->\n         <attr name=\"chatReactionPanelColor\" format=\"color\" /> <!-- update the chat Reaction Background Color only -->\n  <attr name=\"chatReactionPanelCountColor\" format=\"color\" /><!-- update the chat Reaction Panel reaction's count color -->\n        <attr name=\"chatReactionDisplayCountColor\" format=\"color\" /><!-- update the text color of total reactions count in chat message -->\n   <attr name=\"chatReactionFlagTintColor\" format=\"color\" /><!-- update the flag icon tint color in chat reaction panel -->\n  <attr name=\"chatReactionMessageBubbleHighlightedBackground\" format=\"reference\" /><!-- update the color of message bubble on selected -->\n        <attr name=\"chatReactionMessageBackHighlightedBackground\" format=\"reference|color\" /><!-- update the color of message back on selected -->\n        <item name=\"chatInputBackground\">@drawable/rounded_color_input_background</item><!-- update the background of chatInput with drawable/color -->\n        <item name=\"showChatAvatarLogo\">true</item> <!-- show/hide the user display image in chat message -->\n        <item name=\"chatAvatarCircle\">false</item> <!-- circle the user display image in the chat message -->\n  <!-- update the size of user display image -->\n        <item name=\"chatAvatarHeight\">36dp</item>\n        <item name=\"chatAvatarWidth\">32dp</item>\n  <!-- update the size of user display image -->\n        <item name=\"chatAvatarGravity\">top</item> <!-- update the gravity position of the user avatar -->\n  <! -- update the margin of user display image -->\n        <item name=\"chatAvatarMarginLeft\">16dp</item>\n        <item name=\"chatAvatarMarginRight\">0dp</item>\n        <item name=\"chatAvatarMarginBottom\">0dp</item>\n        <item name=\"chatAvatarMarginTop\">1dp</item>\n  <!-- update the margin of user display image -->\n  <!-- update size of send button -->\n        <item name=\"sendButtonHeight\">38dp</item>\n        <item name=\"sendButtonWidth\">38dp</item>\n  <!-- update size of send button -->\n  <!-- update the padding of send button -->\n        <item name=\"chatSendButtonPaddingLeft\">2dp</item>\n        <item name=\"chatSendButtonPaddingRight\">2dp</item>\n        <item name=\"chatSendButtonPaddingTop\">0dp</item>\n        <item name=\"chatSendButtonPaddingBottom\">0dp</item>\n  <!-- update the padding of send button -->\n        <item name=\"userPicDrawable\">@drawable/ic_user_pic</item><!-- placeholder for user display image in chat message -->\n        <item name=\"chatSendDrawable\">@drawable/ic_send_turner</item><!-- update the send button image -->\n        <item name=\"chatSendBackground\">@drawable/send_chat_blue_circle_back</item><!-- Background of send message Button -->\n  <!-- update the padding of the chat bubble -->\n        <item name=\"chatBubblePaddingLeft\">8dp</item>\n        <item name=\"chatBubblePaddingRight\">8dp</item>\n        <item name=\"chatBubblePaddingTop\">8dp</item>\n        <item name=\"chatBubblePaddingBottom\">8dp</item>\n  <!-- update the padding of the chat bubble -->\n        <item name=\"chatReactionPadding\">8dp</item><!-- update the internal padding of chatReaction View -->\n    <item name=\"stickerSelectedTabIndicatorColor\">@color/livelike_black</item><!-- update the sticker keyboard tab indicator color -->\n        <item name=\"stickerTabBackground\">@color/livelike_white</item><!-- update the sticker keyboard tabs background -->\n        <item name=\"stickerBackground\">@color/livelike_white</item><!-- update the sticker keyboard background color or drawable -->\n        <item name=\"stickerRecentEmptyTextColor\">@color/livelike_black</item><!-- update the sticker keyboard empty recent chat text message color -->\n   <item name=\"chatMessageTopBorderHeight\">1dp</item><!--update height of top border of chat message box -->\n        <item name=\"chatMessageTopBorderColor\">#efeff4</item><!-- update color of top border of chat message box --> \t\t\t\n  <item name=\"chatMessageBottomBorderHeight\">1dp</item><!--update height of bottom border of chat message box -->\n        <item name=\"chatMessageBottomBorderColor\">#efeff4</item><!-- update color of bottom border of chat message box -->\n  <item name=\"chatReactionHintEnable\">true</item><!--enable/diable reaction hint in chat message box -->\n   <item name=\"chatReactionIcon\">@drawable/ic_chat_reaction_turner</item><!--update the reaction hint icon in chat message box -->\n  <item name=\"showStickerSend\">true</item><!--show/hide the sticker keyboard icon in chat input box -->\n  <item name=\"showMessageTime\">true</item><!--show/hide message time in the chat message box -->\n  <item name=\"sendIconTintColor\">@color/black</item><!--update the color of icon in the send message button -->\n  <item name=\"stickerIconTintColor\">@color/black</item><!-- update the color of the icon of the sticker keyboard -->\n  <item name=\"chatBubbleWidth\">match_parent</item><!-- update the width of chat bubble,it is not the entire message box only the bubble which exclude the chat avatar -->\n  <item name=\"chatBackgroundWidth\">wrap_content</item><!-- update the width of the chat message box the entire box which include chat avatar and message bubble -->\n  <!-- update the margin for chat bubble in the message box -->\n  \t<item name=\"chatBubbleMarginLeft\">10dp</item>\n  \t<item name=\"chatBubbleMarginTop\">10dp</item>\n  \t<item name=\"chatBubbleMarginRight\">10dp</item>\n  \t<item name=\"chatBubbleMarginBottom\">10dp</item>\n  <!-- update the margin for chat bubble in the message box -->\n  <item name=\"chatSelectedReactionRadius\">12dp<item><!-- update the radius of the selected reaction in the reaction popup -->\n    <item name=\"chatStickerSendDrawable\">@drawable/sticker_icon</item><!-- update the sticker icon in the message input box -->\n     <item name=\"chatStickerKeyboardSendDrawable\">@drawable/keyboard_icon</item><!-- update the keyboard icon in the message input box -->\n    <item name=\"chatAvatarRadius\">15dp</item><!--update the radius of the chat avatar -->\n    <item name=\"rankValueTextColor\">@color/white</item><!-- update the text color of the rank show in the chat view -->\n            <item name=\"chatMessageBottomBorderHeight\">1dp</item><!-- update the height of  bottom of message box -->\n        <item name=\"chatMessageBottomBorderColor\">#efeff4</item><!-- update the border color of bottom of message box -->\n    <item name=\"chatReactionIcon\">@drawable/ic_update_chat_reaction</item><!-- update the reaction icon show at top-right of message box-->\n        <item name=\"chatReactionHintEnable\">true</item><!-- to show the reaction icon at the message box -->\n        <item name=\"chatReactionIconsMarginTop\">15dp</item><!-- margins of reaction icons shown at top-right of the message box by default -->\n        <item name=\"chatReactionIconsMarginBottom\">10dp</item>\n        <item name=\"chatReactionIconPositionBottom\">true</item>\n        <item name=\"chatReactionCountMarginTop\">13dp</item><!-- margins of the reaction count show at message box -->\n        <item name=\"chatReactionCountMarginBottom\">11dp</item>\n        <item name=\"chatReactionCountIconsPositionBottom\">true</item><!-- to show the reaction count with icons positions at bottom of message box -->\n        <item name=\"chatReactionIconsGapFactor\">0.93</item><!-- the gap between the reaction icons shown at top message box, it is the factor which will define the gap with standard width, to overlay the icons use factor value less than 1 and to show gap use factor value greater than 1  -->\n        <item name=\"chatReactionModerationFlagVisible\">false</item><!-- to show/hide the moderation flag icon with reaction panel -->\n        <item name=\"chatUserNameCustomFontPath\">fonts/RingsideExtraWide-Book.otf</item><!-- to set the font of the username of the sender ,it takes file from the asset folder -->\n        <item name=\"chatUserNameTextAllCaps\">true</item><!-- to make all the text of username as capital -->\n        <item name=\"chatUserNameTextSize\">12sp</item><!-- set the textsize of username -->\n        <item name=\"chatMessageCustomFontPath\">fonts/RingsideRegular-Book.otf</item><!-- to set he custom font of message -->\n        <item name=\"chatMessageTextSize\">14sp</item><!-- to set the textsize of message -->\n        <item name=\"chatMessageTimeTextSize\">10sp</item><!-- to update the textsize of the time of the message-->\n        <item name=\"chatMessageTimeCustomFontPath\">fonts/RingsideRegular-Book.otf</item><!-- to set the font of the time of the message -->\n        <item name=\"chatMessageTimeTextAllCaps\">true</item><!-- to make all text capital of time of message -->\n        <item name=\"chatMessageTimeTextColor\">#000000</item><!-- to udpate the textcolor of message time -->\n        <item name=\"chatReactionDisplayCountTextSize\">10sp</item><!-- to update the text size of the count of reactions in message -->\n        <item name=\"chatReactionDisplayCountCustomFontPath\">fonts/RingsideExtraWide-Black.otf</item><!-- to set the font of the reaction count of the message -->\n        <item name=\"chatReactionDisplayCountTextStyle\">bold</item><!-- to set the textstyle of the reaction count of the message -->\n        <item name=\"chatReactionDisplaySize\">12dp</item><!-- to update the size of the reaction icons -->\n        <item name=\"chatReactionPanelGravity\">right|bottom</item><!-- to set the gravity of the reaction panel w.r.t the message box -->\n        <item name=\"chatReactionPanelCountColor\">@color/mml_chat_text_color</item><!-- to update the color of count shown in reaction panel for every reaction -->\n        <item name=\"chatReactionPanelCountCustomFontPath\">fonts/RingsideExtraWide-Black.otf</item><!-- to set the font of count shown in reaction panel for every reaction -->\n    <item name=\"chatReactionPanelCountVisibleIfZero\">false</item><!-- to set the visibility of reaction count on Reaction panel if value is zero -->\n        <item name=\"chatMessageTimeTextLetterSpacing\">0.1</item><!--set the letter spacing of chat message time -->\n        <item name=\"chatMessageTextLetterSpacing\">0.0</item><!--set the letter spacing of chat message -->\n        <item name=\"chatUserNameTextLetterSpacing\">0.0</item><!--set the letter spacing of chat username -->\n    <item name=\"chatInputMaxCharLimit\">250<item> <!-- set the max character limit over the chatInputField -->\n    </style>",
      "language": "xml"
    }
  ]
}
[/block]
**Chat Bubble**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2f8f928-Screenshot_2021-02-25_at_12.14.10_PM.png",
        "Screenshot 2021-02-25 at 12.14.10 PM.png",
        650,
        924,
        "#222529"
      ]
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": " <item name=\"chatWidth\">match_parent</item><!-- to update the width od chat bubble -->\n        <item name=\"chatBubbleBackground\">#FFF</item><!-- to update the background of chat bubble,it can be drawable/color -->\n  <item name=\"chatReactionMessageBubbleHighlightedBackground\">@color/yellow</item> <!-- update the color of message bubble on selected -->\n<item name=\"chatBubbleWidth\">match_parent</item><!-- update the width of chat bubble,it is not the entire message box only the bubble which exclude the chat avatar -->\n  <item name=\"chatBackgroundWidth\">wrap_content</item><!-- update the width of the chat message box the entire box which include chat avatar and message bubble -->\n  <!-- update the margin for chat bubble in the message box -->\n  \t<item name=\"chatBubbleMarginLeft\">10dp</item>\n  \t<item name=\"chatBubbleMarginTop\">10dp</item>\n  \t<item name=\"chatBubbleMarginRight\">10dp</item>\n  \t<item name=\"chatBubbleMarginBottom\">10dp</item>\n  <!-- update the margin for chat bubble in the message box -->\n <!-- update the padding of the chat bubble -->\n        <item name=\"chatBubblePaddingLeft\">8dp</item>\n        <item name=\"chatBubblePaddingRight\">8dp</item>\n        <item name=\"chatBubblePaddingTop\">8dp</item>\n        <item name=\"chatBubblePaddingBottom\">8dp</item>\n  <!-- update the padding of the chat bubble -->",
      "language": "xml"
    }
  ]
}
[/block]
**Send Button**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/069e762-Screenshot_2021-02-25_at_12.44.34_PM.png",
        "Screenshot 2021-02-25 at 12.44.34 PM.png",
        652,
        918,
        "#222529"
      ]
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": " <!-- update size of send button -->\n        <item name=\"sendButtonHeight\">38dp</item>\n        <item name=\"sendButtonWidth\">38dp</item>\n  <!-- update size of send button -->\n  <!-- update the padding of send button -->\n        <item name=\"chatSendButtonPaddingLeft\">2dp</item>\n        <item name=\"chatSendButtonPaddingRight\">2dp</item>\n        <item name=\"chatSendButtonPaddingTop\">0dp</item>\n        <item name=\"chatSendButtonPaddingBottom\">0dp</item>\n  <!-- update the padding of send button -->\n <item name=\"chatSendDrawable\">@drawable/ic_send_turner</item><!-- update the send button image -->\n        <item name=\"chatSendBackground\">@drawable/send_chat_blue_circle_back</item><!-- Background of send message Button -->\n <item name=\"sendIconTintColor\">@color/black</item><!--update the color of icon in the send message button -->",
      "language": "xml"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Upgrade Notes after 2.44 release",
  "body": "**reaction_hint_enable** changed to **chatReactionHintEnable** \n**reaction_icon** changed to **chatReactionIcon** \n**reaction_icons_margin_left** to **chatReactionIconsMarginLeft**\n**reaction_icons_margin_bottom** to **chatReactionIconsMarginBottom**\n**reaction_icons_margin_right** to **chatReactionIconsMarginRight**\n**reaction_icons_margin_top** to **chatReactionIconsMarginTop**\n**reaction_count_margin_left** to **chatReactionCountMarginLeft**\n**reaction_count_margin_bottom** to **chatReactionCountMarginBottom**\n**reaction_count_margin_right** to **chatReactionCountMarginRight**\n**reaction_count_margin_top** to **chatReactionCountMarginTop**\n**reaction_icon_position_bottom** to **chatReactionIconPositionBottom**\n**reaction_count_icons_position_bottom** to **chatReactionCountIconsPositionBottom**\n**reaction_icons_gap_factor** to **chatReactionIconsGapFactor**\n"
}
[/block]
**After that apply the style to your ChatView** 
[block:code]
{
  "codes": [
    {
      "code": "<com.livelike.engagementsdk.chat.ChatView\n        android:id=\"@+id/chat_view\"\n        android:layout_width=\"0dp\"\n        android:layout_height=\"0dp\"\n        style=\"@style/CustomChatTheme\"\n        app:layout_constraintBottom_toBottomOf=\"parent\"\n        app:layout_constraintEnd_toEndOf=\"parent\"\n        app:layout_constraintStart_toStartOf=\"parent\"\n        app:layout_constraintTop_toTopOf=\"parent\" />",
      "language": "xml"
    }
  ]
}
[/block]
**ChatView External Media**
To Allow user of external media in the ChatView, you need to set the variable value to true
for example :
chat_view.allowMediaFromKeyboard = true  

Note: By Default the allowMediaFromKeyboard is true

**Snap to Live Button**
To update the position of the snap to Live button set the values in their respective files which will override the values of SDK.
1. dimens: livelike_snap_live_width,livelike_snap_live_height,livelike_snap_live_horizontal_bias(float),livelike_snap_live_radius,livelike_snap_live_elevation,livelike_snap_live_margin_start,livelike_snap_live_margin_left,livelike_snap_live_margin_end,livelike_snap_live_margin_right,livelike_snap_live_margin_bottom
2. colors: livelike_snap_live_icon_color,livelike_snap_live_color
3. drawable: ic_chat_ic_live.png

[block:api-header]
{
  "title": "Chat: Message Timestamp Display"
}
[/block]
To update the message timestamp textview text color and font.
[block:code]
{
  "codes": [
    {
      "code": "\n<color name=\"livelike_chatMessage_timestamp_text_color\">#666666</color>\n\n<item name=\"livelike_chatMessage_timestamp_text_font\"    \ntype=\"font\">@font/roboto_regular</item>",
      "language": "xml"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Overriding Widget Animations"
}
[/block]
You can also override the default Lottie animations for some widgets. To do this you need to do the following:
1. Create a folder inside the assets folder.
2. Provide the folder name to the `winAnimation` and `loseAnimation` tags as shown below:
[block:code]
{
  "codes": [
    {
      "code": "<item name=\"winAnimation\">@string/win_animation</item><!-- name of the folder inside assets folder where win animations are placed -->\n<item name=\"loseAnimation\">@string/lose_animation</item><!-- name of the folder inside assets folder where lose animations are placed -->",
      "language": "xml"
    }
  ]
}
[/block]
3. You can provide 1 or more custom animations. If more than 1 animation is provided we will cycle through those in random order.

Instructions for creating the Lottie animations can be found in the [Lottie Animation Guidelines](lottie-animation-guidelines).