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

## Widget Theming

You can theme widgets in a variety of different ways as shown below:

![729](https://files.readme.io/6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif "Screen Recording 2019-09-16 at 04.23 PM.gif")

![726](https://files.readme.io/ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif "Screen Recording 2019-09-16 at 04.24 PM.gif")

![725](https://files.readme.io/16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif "Screen Recording 2019-09-16 at 04.24 PM (1).gif")

On Android, you can override the default values of colors, fonts, and dimensions in the values folder of the SDK. The customizable variables and their functions are listed below:

### Colors

You can override the color values by setting your own. The default values for the SDK are listed in the **colors.xml** resource file.

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
  <summary>Common</summary>
  <br>
  <p><code>livelike_default_text_color</code> : Default color for all text in the SDK.</p>
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Widget Headers</summary>
<br>
<p>These control the gradient colors of the title. You can set them to be the same to get a single solid color title background.</p>
<br>
  <p><code>livelike_header_text_color</code> : The color of the title text in a widget, same as default text color</p>
  <br>
  <p>Poll View</p>
  <ul>
    <li>* <code>livelike_poll_title_gradient_left</code> </li>
    <li>* <code>livelike_poll_title_gradient_right</code> </li>
  </ul>  
<br>
  <p>Quiz View</p>
  <ul>
  <li>* <code>livelike_quiz_title_gradient_left</code> </li>
  <li>* <code>livelike_quiz_title_gradient_right</code> </li>
  </ul>
  <br>
  <p>Prediction View</p>
  <ul>
    <li>* <code>livelike_prediction_title_gradient_left</code> </li>
    <li>* <code>livelike_prediction_title_gradient_right</code> </li>
  <ul>
<br>
    <p>Emoji Slider</p>
    <ul>
      <li>* <code>livelike_image_slider_header_bg</code></li>
    </ul>   
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->
<details>
<summary>Widget Options</summary>
<br>
<p>Poll Option: These are the colors of percentage bar and border for the poll option view.</p>
<ul>
  <li>* <code>livelike_poll_bar_gradient_left</code></li>
  <li>* <code>livelike_poll_bar_gradient_right</code></li>
  <li>* <code>livelike_poll_option_selected_border</code></li>
</ul>
<br>
  <p>Quiz Option: These are the colors of percentage bar and border for the quiz option view.</p>
  <ul>
    <li>* <code>livelike_quiz_bar_gradient_left</code></li>
    <li>* <code>livelike_quiz_bar_gradient_right</code></li>
    <li>* <code>livelike_quiz_option_selected_border</code></li>
  </ul> 
<br>
  <p>Prediction Option: These are the colors of percentage bar and border for the prediction option view.</p>
  <ul>
    <li>* <code>livelike_prediction_option_selected_border</code></li>
    <li>* <code>livelike_prediction_image_option_selected_border</code></li>
  </ul>  
  <br>
  <p>Not Selected option: These are the colors of percentage bar for the not selected option view for all options.</p>
<ul>
  <li>* <code>livelike_neutral_bar_gradient_left</code></li>
  <li>* <code>livelike_neutral_bar_gradient_right</code></li>
</ul>  
<br>
<p>Text Color:</p>
<ul>
  <li>* <code>livelike_option_text_color</code> : Default text color in the options, same as default text color.</li>
</ul>
<br>
<p>Right and wrong answer percentage bar : For widgets where the percentage bar's and border color is different based on user input:</p>
<ul>
  <li>* <code>livelike_correct_bar_gradient_left</code></li>
  <li>* <code>livelike_correct_bar_gradient_right</code></li>
  <li>* <code>livelike_incorrect_bar_gradient_left</code></li>
  <li>* <code>livelike_incorrect_bar_gradient_right</code></li>
  <li>* <code>livelike_neutral_bar_gradient_left</code></li>
  <li>* <code>livelike_neutral_bar_gradient_right</code></li>
  <li>* <code>livelike_correct_option_border_color</code></li>
  <li>* <code>livelike_incorrect_option_border_color</code></li>
</ul>
 <br>
  <p> Option Background: For updating the background color of every option(not the progress color)</p> 
  <ul>
  <li><code>livelike_default_button_background_color</code></li>
  </ul> 
 <br>
  <p>Emoji Slider: For updating the style of emoji slider</p>
  <ul>
    <li>* <code>livelike_image_slider_gradient_start</code></li>
    <li>* <code>livelike_image_slider_gradient_end</code></li>
    <li>* <code>livelike_image_slider_bg</code></li>
    <li>* <code>livelike_image_slider_widget_result_end_color</code></li>
    <li>* <code>livelike_image_slider_widget_result_center_color</code></li>
  </ul>  
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Alert Widget</summary>
<br>
<p><strong>Header</strong><p>
  <p>The title bar's background color gradients:</p>
  <ul>
    <li>* <code>livelike_alert_notification_label_gradient_left</code></li>
    <li>* <code>livelike_alert_notification_label_gradient_right</code></li>
    <li>* <code>livelike_alert_label_background_shadow</code> : Shadow color of the title</li>
    <br>
    <p> To have custom background with customize drawable ,create a drawable with name <code>alert_notification_label_background.xml</code> ,this will override the current header background with your drawable.</p>
  </ul>
  <br>
  <p><strong>Body</strong></p>
  <p>Background Color:</p>
  <ul>
    <li>* <code>livelike_alert_background_gradient_left</code></li>
    <li>* <code>livelike_alert_background_gradient_right</code></li>
    <br>
    <p>Text Color:</p>
    <li>* <code>livelike_alert_body_text_color</code> : The color of the body text of the alert</li>
    <li>* <code>livelike_alert_link_text_color</code> : Color of the link text</li>
    <li>* <code>livelike_alert_label_text_color</code> : Color of the header text</li>
  </ul>
  </details>

<br>
`}</HTMLBlock>

### Fonts

Font size can be controlled via the variables listed in **dimens.xml**.

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Common</summary>
<br>
<ul>
  <li>* <code>livelike_header_text_size</code> : The font size of the header text.</li>
  <li>* <code>livelike_option_text_size</code> : The font size of the options text.</li>
  <li>* <code>livelike_percent_label_text_size</code> : The percentage bar text size.</li>
</ul>
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Alert Widget</summary>
<br>
<ul>
  <li>* <code>livelike_alert_body_text_size</code> : Alert widget body text size.</li>
  <li>* <code>livelike_alert_link_text_size</code> : Alert link text size.</li>
  <li>* <code>livelike_alert_label_text_size</code> : Alert label text size.</li>
</ul>
</details>

<br>
`}</HTMLBlock>

### Other

These include variables like border radius and stroke width of most ui elements.

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Details</summary>
<br>
<ul>
  <li>* <code>livelike_percent_bar_corner_radius</code></li>
  <li>* <code>livelike_percent_bar_corner_radius_image</code></li>
  <li>* <code>livelike_header_corner_radius</code></li>
  <li>* <code>livelike_header_background_notification_label_radius</code></li>
  <li>* <code>livelike_chat_rounded_rect_radius</code></li>
  <li>* <code>livelike_button_corner_radius</code></li>
  <li>* <code>livelike_button_outline_stroke_width</code></li>
  <li>* <code>livelike_confirm_outline_stroke_width</code></li>
  <li>* <code>livelike_header_outline_stroke_width</code></li>
</ul>
</details>

<br>
`}</HTMLBlock>

## Chat Theming

Just like the widgets, the chat component is also customizable through overriding the default values provided in the dimens/colors/attrs xml files with values in XML files in the integrating application. The variables available for customization are listed below:

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Chat View</summary>
<br>
<p>The chat view is designed to fill the parent view. So its height and width can be controlled directly by the integrator by controlling the height and width of the view provided by them.</p>
<p><strong>Background</strong></p>
<p>Gradient start and end color:</p>
<ul>
  <li>* <code>livelike_chat_background_end_color</code>, color</li>
  <li>* <code>livelike_chat_background_start_color</code>, color</li>
</ul>
<br>
<p>Gradient angle:</p>
<ul>
  <li>* <code>livelike_chat_background_gradient_angle</code>, integer</li>
</ul>
<br>
<p><strong>Username</strong></p>
<p>Default color of the text:</p>
<ul>
  <li>* <code>livelike_openChatNicknameOther</code>, color</li>
</ul>
<br>
<p>Color of the text if message sent by current user:</p>
<ul>
  <li>* <code>livelike_openChatNicknameMe</code>, color</li>
</ul>
<br>
<p>Font size of the text:</p>
<ul>
  <li>* <code>livelike_default_chat_cell_name_size</code>, dimen</li>
</ul>
<br>
<p><strong>Message</strong></p>
<p>Text color:</p>
<ul>
  <li>* <code>livelike_default_chat_cell_message_color</code>, color</li>
</ul><br>
<p>Text font size:</p>
<ul>
  <li>* <code>livelike_default_chat_cell_text_size</code>, dimen</li>
</ul><br>
<p><strong>Chat Bubble</strong></p>
<p>Border radius of chat bubble:</p>
<ul>
  <li>* <code>livelike_chat_rounded_rect_radius</code>, dimen</li>
</ul><br>
<p>Background color of the chat message:</p>
<ul>
  <li>* <code>livelike_chat_rounded_rect_color</code>, color</li>
</ul><br>
<p>Padding (Horizontal/Vertical):</p>
<ul>
  <li>* <code>livelike_default_chat_cell_padding_horizontal</code>, dimen</li><br>
  <li>* <code>livelike_default_chat_cell_padding_vertical</code>, dimen</li>
</ul><br>
<p>Padding (Each Side):</p>
<ul>
  <li>* <code>livelike_default_chat_cell_padding_left</code>, dimen</li>
  <li>* <code>livelike_default_chat_cell_padding_right</code>, dimen</li>
  <li>* <code>livelike_default_chat_cell_padding_top</code>, dimen</li>
  <li>* <code>livelike_default_chat_cell_padding_bottom</code>, dimen</li>
</ul><br>
<p>Margin:</p>
<ul>
  <li>* <code>livelike_default_chat_cell_margin_vertical</code>, dimen</li>
</ul><br>
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Chat Input</summary>
<br>
<ul>
<li>* Font size: <code>livelike_default_chat_input_text_size</code>, dimen</li>

<li>* Font color: <code>livelike_chat_input_text_color</code>, color</li>

<li>* Background Color: <code>livelike_chat_input_background_color</code>, color</li>

<li>* Border Radius: <code>livelike_default_chat_input_border_radius</code>, dimen</li>

<li>* Border Color: <code>livelike_chat_input_border_color</code>, color</li>

<li>* Border Width: <code>livelike_default_chat_input_border_stroke</code>, dimen</li>

<li>* Margin: <code>livelike_default_chat_input_margin_bottom</code>, dimen</li>
</ul>
</details>
`}</HTMLBlock>

<HTMLBlock>{`
<!-- Markdown converted to HTML using a markdown converter such as https://www.browserling.com/tools/markdown-to-html -->

<details>
<summary>Snap To Live</summary>
<br>
<ul>
<li>Background color: <code>livelike_live_button_background_color</code>, color</li>

<li>Arrow color: <code>livelike_live_button_arrow_color</code>, color</li>
</ul>
</details>

<br>
`}</HTMLBlock>

**Advanced Chat Customization**

As an integrator, you are able to customize the look and feel of the experience you provide to your users through the XML custom attributes using in layout. Create the theme and add the attributes you want to update.

```xml
<style name="CustomChatTheme" parent="AppTheme">
        <item name="displayUserProfile">false</item><!-- To display the gamification display in chatView -->
        <item name="chatWidth">match_parent</item><!-- to update the width od chat bubble -->
        <item name="chatBubbleBackground">#FFF</item><!-- to update the background of chat bubble,it can be drawable/color -->
        <item name="chatBackground">#FFF</item><!-- update the background of chat message box,it can be drawable/color -->
        <item name="usernameColor">#000</item><!-- update the color of username in chat message -->
        <item name="otherUsernameColor">#000</item><!-- update the color of different username in chat message -->
        <item name="messageColor">#5f5f5f</item><!-- update color of message in chat message -->
        <item name="chatInputViewBackground">#FFF</item><!-- update the background of ChatInput, it can be drawable/color -->
        <item name="chatDisplayBackground">#efeff4</item><!-- update the background of Chat List, it can be drawable/color  -->
        <item name="chatViewBackground">#FFF</item><!-- update the background of full ChatFull View, it can be drawable/color --> 
        <item name="chatInputTextColor">#8e8e93</item><!-- update the color of textInput -->
        <item name="chatInputTextSize">15sp</item><!-- update the textsize of textInput -->
        <item name="chatInputTextHintColor">#8e8e93</item><!-- update the hint color of textInput -->
  <!--update the margin for chat box -->
        <item name="chatMarginBottom">3dp</item>
        <item name="chatMarginTop">0dp</item>
        <item name="chatMarginLeft">0dp</item>
        <item name="chatMarginRight">0dp</item>
  <!--update the margin for chat box -->
  <!-- update the position of ChatReactionView -->
        <item name="chatReactionXPosition">120dp</item>
        <item name="chatReactionYPosition">25dp</item>
  <!-- update the position of ChatReactionView -->
        <item name="chatReactionElevation">6dp</item><!-- update the elevation of chat reaction (CardView) -->
        <item name="chatReactionRadius">20dp</item> <!-- update the chat Reaction(CardView) View corner radius -->
         <attr name="chatReactionPanelColor" format="color" /> <!-- update the chat Reaction Background Color only -->
  <attr name="chatReactionPanelCountColor" format="color" /><!-- update the chat Reaction Panel reaction's count color -->
        <attr name="chatReactionDisplayCountColor" format="color" /><!-- update the text color of total reactions count in chat message -->
   <attr name="chatReactionFlagTintColor" format="color" /><!-- update the flag icon tint color in chat reaction panel -->
  <attr name="chatReactionMessageBubbleHighlightedBackground" format="reference" /><!-- update the color of message bubble on selected -->
        <attr name="chatReactionMessageBackHighlightedBackground" format="reference|color" /><!-- update the color of message back on selected -->
        <item name="chatInputBackground">@drawable/rounded_color_input_background</item><!-- update the background of chatInput with drawable/color -->
        <item name="showChatAvatarLogo">true</item> <!-- show/hide the user display image in chat message -->
        <item name="chatAvatarCircle">false</item> <!-- circle the user display image in the chat message -->
  <!-- update the size of user display image -->
        <item name="chatAvatarHeight">36dp</item>
        <item name="chatAvatarWidth">32dp</item>
  <!-- update the size of user display image -->
        <item name="chatAvatarGravity">top</item> <!-- update the gravity position of the user avatar -->
  <! -- update the margin of user display image -->
        <item name="chatAvatarMarginLeft">16dp</item>
        <item name="chatAvatarMarginRight">0dp</item>
        <item name="chatAvatarMarginBottom">0dp</item>
        <item name="chatAvatarMarginTop">1dp</item>
  <!-- update the margin of user display image -->
  <!-- update size of send button -->
        <item name="sendButtonHeight">38dp</item>
        <item name="sendButtonWidth">38dp</item>
  <!-- update size of send button -->
  <!-- update the padding of send button -->
        <item name="chatSendButtonPaddingLeft">2dp</item>
        <item name="chatSendButtonPaddingRight">2dp</item>
        <item name="chatSendButtonPaddingTop">0dp</item>
        <item name="chatSendButtonPaddingBottom">0dp</item>
  <!-- update the padding of send button -->
        <item name="userPicDrawable">@drawable/ic_user_pic</item><!-- placeholder for user display image in chat message -->
        <item name="chatSendDrawable">@drawable/ic_send_turner</item><!-- update the send button image -->
        <item name="chatSendBackground">@drawable/send_chat_blue_circle_back</item><!-- Background of send message Button -->
  <!-- update the padding of the chat bubble -->
        <item name="chatBubblePaddingLeft">8dp</item>
        <item name="chatBubblePaddingRight">8dp</item>
        <item name="chatBubblePaddingTop">8dp</item>
        <item name="chatBubblePaddingBottom">8dp</item>
  <!-- update the padding of the chat bubble -->
        <item name="chatReactionPadding">8dp</item><!-- update the internal padding of chatReaction View -->
    <item name="stickerSelectedTabIndicatorColor">@color/livelike_black</item><!-- update the sticker keyboard tab indicator color -->
        <item name="stickerTabBackground">@color/livelike_white</item><!-- update the sticker keyboard tabs background -->
        <item name="stickerBackground">@color/livelike_white</item><!-- update the sticker keyboard background color or drawable -->
        <item name="stickerRecentEmptyTextColor">@color/livelike_black</item><!-- update the sticker keyboard empty recent chat text message color -->
   <item name="chatMessageTopBorderHeight">1dp</item><!--update height of top border of chat message box -->
        <item name="chatMessageTopBorderColor">#efeff4</item><!-- update color of top border of chat message box --> 			
  <item name="chatMessageBottomBorderHeight">1dp</item><!--update height of bottom border of chat message box -->
        <item name="chatMessageBottomBorderColor">#efeff4</item><!-- update color of bottom border of chat message box -->
  <item name="chatReactionHintEnable">true</item><!--enable/diable reaction hint in chat message box -->
   <item name="chatReactionIcon">@drawable/ic_chat_reaction_turner</item><!--update the reaction hint icon in chat message box -->
  <item name="showStickerSend">true</item><!--show/hide the sticker keyboard icon in chat input box -->
  <item name="showMessageTime">true</item><!--show/hide message time in the chat message box -->
  <item name="sendIconTintColor">@color/black</item><!--update the color of icon in the send message button -->
  <item name="stickerIconTintColor">@color/black</item><!-- update the color of the icon of the sticker keyboard -->
  <item name="chatBubbleWidth">match_parent</item><!-- update the width of chat bubble,it is not the entire message box only the bubble which exclude the chat avatar -->
  <item name="chatBackgroundWidth">wrap_content</item><!-- update the width of the chat message box the entire box which include chat avatar and message bubble -->
  <!-- update the margin for chat bubble in the message box -->
  	<item name="chatBubbleMarginLeft">10dp</item>
  	<item name="chatBubbleMarginTop">10dp</item>
  	<item name="chatBubbleMarginRight">10dp</item>
  	<item name="chatBubbleMarginBottom">10dp</item>
  <!-- update the margin for chat bubble in the message box -->
  <item name="chatSelectedReactionRadius">12dp<item><!-- update the radius of the selected reaction in the reaction popup -->
    <item name="chatStickerSendDrawable">@drawable/sticker_icon</item><!-- update the sticker icon in the message input box -->
     <item name="chatStickerKeyboardSendDrawable">@drawable/keyboard_icon</item><!-- update the keyboard icon in the message input box -->
    <item name="chatAvatarRadius">15dp</item><!--update the radius of the chat avatar -->
    <item name="rankValueTextColor">@color/white</item><!-- update the text color of the rank show in the chat view -->
            <item name="chatMessageBottomBorderHeight">1dp</item><!-- update the height of  bottom of message box -->
        <item name="chatMessageBottomBorderColor">#efeff4</item><!-- update the border color of bottom of message box -->
    <item name="chatReactionIcon">@drawable/ic_update_chat_reaction</item><!-- update the reaction icon show at top-right of message box-->
        <item name="chatReactionHintEnable">true</item><!-- to show the reaction icon at the message box -->
        <item name="chatReactionIconsMarginTop">15dp</item><!-- margins of reaction icons shown at top-right of the message box by default -->
        <item name="chatReactionIconsMarginBottom">10dp</item>
        <item name="chatReactionIconPositionBottom">true</item>
        <item name="chatReactionCountMarginTop">13dp</item><!-- margins of the reaction count show at message box -->
        <item name="chatReactionCountMarginBottom">11dp</item>
        <item name="chatReactionCountIconsPositionBottom">true</item><!-- to show the reaction count with icons positions at bottom of message box -->
        <item name="chatReactionIconsGapFactor">0.93</item><!-- the gap between the reaction icons shown at top message box, it is the factor which will define the gap with standard width, to overlay the icons use factor value less than 1 and to show gap use factor value greater than 1  -->
        <item name="chatReactionModerationFlagVisible">false</item><!-- to show/hide the moderation flag icon with reaction panel -->
        <item name="chatUserNameCustomFontPath">fonts/RingsideExtraWide-Book.otf</item><!-- to set the font of the username of the sender ,it takes file from the asset folder -->
        <item name="chatUserNameTextAllCaps">true</item><!-- to make all the text of username as capital -->
        <item name="chatUserNameTextSize">12sp</item><!-- set the textsize of username -->
        <item name="chatMessageCustomFontPath">fonts/RingsideRegular-Book.otf</item><!-- to set he custom font of message -->
        <item name="chatMessageTextSize">14sp</item><!-- to set the textsize of message -->
        <item name="chatMessageTimeTextSize">10sp</item><!-- to update the textsize of the time of the message-->
        <item name="chatMessageTimeCustomFontPath">fonts/RingsideRegular-Book.otf</item><!-- to set the font of the time of the message -->
        <item name="chatMessageTimeTextAllCaps">true</item><!-- to make all text capital of time of message -->
        <item name="chatMessageTimeTextColor">#000000</item><!-- to udpate the textcolor of message time -->
        <item name="chatReactionDisplayCountTextSize">10sp</item><!-- to update the text size of the count of reactions in message -->
        <item name="chatReactionDisplayCountCustomFontPath">fonts/RingsideExtraWide-Black.otf</item><!-- to set the font of the reaction count of the message -->
        <item name="chatReactionDisplayCountTextStyle">bold</item><!-- to set the textstyle of the reaction count of the message -->
        <item name="chatReactionDisplaySize">12dp</item><!-- to update the size of the reaction icons -->
        <item name="chatReactionPanelGravity">right|bottom</item><!-- to set the gravity of the reaction panel w.r.t the message box -->
        <item name="chatReactionPanelCountColor">@color/mml_chat_text_color</item><!-- to update the color of count shown in reaction panel for every reaction -->
        <item name="chatReactionPanelCountCustomFontPath">fonts/RingsideExtraWide-Black.otf</item><!-- to set the font of count shown in reaction panel for every reaction -->
    <item name="chatReactionPanelCountVisibleIfZero">false</item><!-- to set the visibility of reaction count on Reaction panel if value is zero -->
        <item name="chatMessageTimeTextLetterSpacing">0.1</item><!--set the letter spacing of chat message time -->
        <item name="chatMessageTextLetterSpacing">0.0</item><!--set the letter spacing of chat message -->
        <item name="chatUserNameTextLetterSpacing">0.0</item><!--set the letter spacing of chat username -->
    <item name="chatInputMaxCharLimit">250<item> <!-- set the max character limit over the chatInputField -->
    </style>
```

**Chat Bubble**

![650](https://files.readme.io/2f8f928-Screenshot_2021-02-25_at_12.14.10_PM.png "Screenshot 2021-02-25 at 12.14.10 PM.png")

```xml
<item name="chatWidth">match_parent</item><!-- to update the width od chat bubble -->
        <item name="chatBubbleBackground">#FFF</item><!-- to update the background of chat bubble,it can be drawable/color -->
  <item name="chatReactionMessageBubbleHighlightedBackground">@color/yellow</item> <!-- update the color of message bubble on selected -->
<item name="chatBubbleWidth">match_parent</item><!-- update the width of chat bubble,it is not the entire message box only the bubble which exclude the chat avatar -->
  <item name="chatBackgroundWidth">wrap_content</item><!-- update the width of the chat message box the entire box which include chat avatar and message bubble -->
  <!-- update the margin for chat bubble in the message box -->
  	<item name="chatBubbleMarginLeft">10dp</item>
  	<item name="chatBubbleMarginTop">10dp</item>
  	<item name="chatBubbleMarginRight">10dp</item>
  	<item name="chatBubbleMarginBottom">10dp</item>
  <!-- update the margin for chat bubble in the message box -->
 <!-- update the padding of the chat bubble -->
        <item name="chatBubblePaddingLeft">8dp</item>
        <item name="chatBubblePaddingRight">8dp</item>
        <item name="chatBubblePaddingTop">8dp</item>
        <item name="chatBubblePaddingBottom">8dp</item>
  <!-- update the padding of the chat bubble -->
```

**Send Button**

![652](https://files.readme.io/069e762-Screenshot_2021-02-25_at_12.44.34_PM.png "Screenshot 2021-02-25 at 12.44.34 PM.png")

```xml
<!-- update size of send button -->
        <item name="sendButtonHeight">38dp</item>
        <item name="sendButtonWidth">38dp</item>
  <!-- update size of send button -->
  <!-- update the padding of send button -->
        <item name="chatSendButtonPaddingLeft">2dp</item>
        <item name="chatSendButtonPaddingRight">2dp</item>
        <item name="chatSendButtonPaddingTop">0dp</item>
        <item name="chatSendButtonPaddingBottom">0dp</item>
  <!-- update the padding of send button -->
 <item name="chatSendDrawable">@drawable/ic_send_turner</item><!-- update the send button image -->
        <item name="chatSendBackground">@drawable/send_chat_blue_circle_back</item><!-- Background of send message Button -->
 <item name="sendIconTintColor">@color/black</item><!--update the color of icon in the send message button -->
```

> 📘 Upgrade Notes after 2.44 release
>
> **reaction\_hint\_enable** changed to **chatReactionHintEnable**\
> **reaction\_icon** changed to **chatReactionIcon**\
> **reaction\_icons\_margin\_left** to **chatReactionIconsMarginLeft**\
> **reaction\_icons\_margin\_bottom** to **chatReactionIconsMarginBottom**\
> **reaction\_icons\_margin\_right** to **chatReactionIconsMarginRight**\
> **reaction\_icons\_margin\_top** to **chatReactionIconsMarginTop**\
> **reaction\_count\_margin\_left** to **chatReactionCountMarginLeft**\
> **reaction\_count\_margin\_bottom** to **chatReactionCountMarginBottom**\
> **reaction\_count\_margin\_right** to **chatReactionCountMarginRight**\
> **reaction\_count\_margin\_top** to **chatReactionCountMarginTop**\
> **reaction\_icon\_position\_bottom** to **chatReactionIconPositionBottom**\
> **reaction\_count\_icons\_position\_bottom** to **chatReactionCountIconsPositionBottom**\
> **reaction\_icons\_gap\_factor** to **chatReactionIconsGapFactor**

**After that apply the style to your ChatView** 

```xml
<com.livelike.engagementsdk.chat.ChatView
        android:id="@+id/chat_view"
        android:layout_width="0dp"
        android:layout_height="0dp"
        style="@style/CustomChatTheme"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

**ChatView External Media**\
To Allow user of external media in the ChatView, you need to set the variable value to true\
for example :\
chat\_view\.allowMediaFromKeyboard = true  

Note: By Default the allowMediaFromKeyboard is true

**Snap to Live Button**\
To update the position of the snap to Live button set the values in their respective files which will override the values of SDK.

1. dimens: livelike\_snap\_live\_width,livelike\_snap\_live\_height,livelike\_snap\_live\_horizontal\_bias(float),livelike\_snap\_live\_radius,livelike\_snap\_live\_elevation,livelike\_snap\_live\_margin\_start,livelike\_snap\_live\_margin\_left,livelike\_snap\_live\_margin\_end,livelike\_snap\_live\_margin\_right,livelike\_snap\_live\_margin\_bottom
2. colors: livelike\_snap\_live\_icon\_color,livelike\_snap\_live\_color
3. drawable: ic\_chat\_ic\_live.png

## Chat: Message Timestamp Display

To update the message timestamp textview text color and font.

```xml
<color name="livelike_chatMessage_timestamp_text_color">#666666</color>

<item name="livelike_chatMessage_timestamp_text_font"    
type="font">@font/roboto_regular</item>
```

## Overriding Widget Animations

You can also override the default Lottie animations for some widgets. To do this you need to do the following:

1. Create a folder inside the assets folder.
2. Provide the folder name to the `winAnimation` and `loseAnimation` tags as shown below:

```xml
<item name="winAnimation">@string/win_animation</item><!-- name of the folder inside assets folder where win animations are placed -->
<item name="loseAnimation">@string/lose_animation</item><!-- name of the folder inside assets folder where lose animations are placed -->
```

3. You can provide 1 or more custom animations. If more than 1 animation is provided we will cycle through those in random order.

Instructions for creating the Lottie animations can be found in the [Lottie Animation Guidelines](lottie-animation-guidelines).
