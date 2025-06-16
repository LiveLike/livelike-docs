---
title: Play Predictor Events
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Below is a list of analytics events triggered in Play Predictor, along with their details.  

> **Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/react-vxwfaksw?file=analytics-service.js), where event listeners have been integrated and forwarded to Google Analytics (GA).  

### **Event List**

[block:parameters]
{
  "data": {
    "h-0": "**Event Name**",
    "h-1": "**Event Trigger Condition**",
    "h-2": "**Event Properties**  \n_(not included default event properties as outlined [here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_",
    "h-3": "**Event Description**",
    "0-0": "**session_start**",
    "0-1": "When the user starts a web session.",
    "0-2": "—",
    "0-3": "Marks the beginning of a session.",
    "1-0": "**session_stop**",
    "1-1": "When the user exits the web session.",
    "1-2": "`duration` (in seconds)",
    "1-3": "Tracks the total session length.",
    "2-0": "**visit_page**",
    "2-1": "When the user visits any page.",
    "2-2": "`page_name`  \n(fixtures, predictor_play, predictor_edit_predictions, predictor_see_results, predictor_awaiting_results, welcome, info, profile, leaderboard)",
    "2-3": "Tracks user navigation between pages.",
    "3-0": "**view_fixture**",
    "3-1": "When the user views a fixture card.",
    "3-2": "`fixture_details`  \n(team names, date, start time)  \n`fixture_state`  \n(predict_now, edit_now, awaiting_results, see_results, upcoming/locked)  \n`ll_program_name`  \n`ll_program_id`",
    "3-3": "Captures when users view match fixtures.",
    "4-0": "**interact_fixture**",
    "4-1": "When the user interacts with a fixture card.",
    "4-2": "`fixture_details`  \n`fixture_state` (play, edit_prediction, awaiting_results, locked, see_results)  \n`ll_program_name`  \n`ll_program_id`",
    "4-3": "Tracks interactions like making or editing predictions.",
    "5-0": "**widget_viewed**",
    "5-1": "When the user views a question widget.",
    "5-2": "`widget_type` (image prediction, text quiz, text_prediction_follow_up)  \n`widget_state` (active, submitted, expired, result)  \n`question_type` (head-to-head, slider, match score)  \n`question_name`  \n`ll_program_name`  \n`ll_program_id`",
    "5-3": "Tracks when users see a prediction question.",
    "6-0": "**widget_interacted**",
    "6-1": "When the user submits a response to a widget.",
    "6-2": "`widget_type` (image prediction, text quiz, text_poll)  \n`widget_state`  \n`question_type`  \n`question_name`  \n`option_index`  \n`option_submitted`  \n `ll_program_name`  \n`ll_program_id`",
    "6-3": "Captures user engagement with prediction widgets.",
    "7-0": "**prediction_result**",
    "7-1": "When the user views the prediction follow-up widget.",
    "7-2": "`widget_type` (image_prediction_follow_up, text_prediction_follow_up)  \n`question_type`  \n`question_name`  \n`option_submitted`  \n`is_correct` (true/false)  \n`ll_program_name`  \n`ll_program_id`",
    "7-3": "Tracks when users see their prediction results.",
    "8-0": "**nickname_change**",
    "8-1": "When the user confirms a nickname change.",
    "8-2": "`source_page` (welcome, profile)  \n`old_name`  \n`new_name`",
    "8-3": "Logs nickname changes if applicable.",
    "9-0": "**click_sponsor**",
    "9-1": "When the user clicks a sponsor logo (if clickable).",
    "9-2": "`sponsor_id`  \n`sponsor_name`  \n`sponsor_url`",
    "9-3": "Tracks sponsor interactions."
  },
  "cols": 4,
  "rows": 10,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]