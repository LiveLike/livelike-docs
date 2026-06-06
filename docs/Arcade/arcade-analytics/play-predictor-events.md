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

| **Event Name**         | **Event Trigger Condition**                          | **Event Properties**_(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_                                                                                                                                                                 | **Event Description**                                   |
| :--------------------- | :--------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------ |
| **session\_start**     | When the user starts a web session.                  | —                                                                                                                                                                                                                                                                                                                   | Marks the beginning of a session.                       |
| **session\_stop**      | When the user exits the web session.                 | `duration` (in seconds)                                                                                                                                                                                                                                                                                             | Tracks the total session length.                        |
| **visit\_page**        | When the user visits any page.                       | `page_name`<br />(fixtures, predictor\_play, predictor\_edit\_predictions, predictor\_see\_results, predictor\_awaiting\_results, welcome, info, profile, Leaderboard)                                                                                                                                              | Tracks user navigation between pages.                   |
| **view\_fixture**      | When the user views a fixture card.                  | `fixture_details`<br />(team names, date, start time)<br />`fixture_state`<br />(predict\_now, edit\_now, awaiting\_results, see\_results, upcoming/locked)<br />`ll_program_name`<br />`ll_program_id`                                                                                                             | Captures when users view match fixtures.                |
| **click\_play**        | When the user interacts with a fixture card.         | `fixture_details`<br />`fixture_state` (play, edit\_prediction, awaiting\_results, locked, see\_results)<br />`ll_program_name`<br />`ll_program_id`                                                                                                                                                                | Tracks interactions like making or editing predictions. |
| **widget\_viewed**     | When the user views a question widget.               | `widget_type` (image prediction, text quiz, text\_prediction\_follow\_up)<br />`widget_state` (active, submitted, expired, result)<br />`question_type` (head-to-head, slider, match score)<br />`question_name`<br />`ll_program_name`<br />`ll_program_id`                                                        | Tracks when users see a prediction question.            |
| **widget\_interacted** | When the user submits a response to a widget.        | `widget_type` (image prediction, text quiz, text\_poll)<br />`widget_state`(active, submitted, expired, result)<br />`question_type`(head-to-head, slider, match score)<br />`question_name`<br />`option_index`<br />`option_submitted`<br />`is_correct` (true/false)<br />`ll_program_name`<br />`ll_program_id` | Captures user engagement with prediction widgets.       |
| **prediction\_result** | When the user views the prediction follow-up widget. | `widget_type` (image\_prediction\_follow\_up, text\_prediction\_follow\_up)<br />`question_type`(head-to-head, slider, match score)<br />`question_name`<br />`option_submitted`<br />`is_correct` (true/false)<br />`ll_program_name`<br />`ll_program_id`                                                         | Tracks when users see their prediction results.         |
| **nickname\_change**   | When the user confirms a nickname change.            | `source_page` (welcome, profile)<br />`old_name`<br />`new_name`                                                                                                                                                                                                                                                    | Logs nickname changes if applicable.                    |
| **click\_sponsor**     | When the user clicks a sponsor logo (if clickable).  | `sponsor_id`<br />`sponsor_name`<br />`sponsor_url`                                                                                                                                                                                                                                                                 | Tracks sponsor interactions.                            |
| **game\_completed**    | Triggers when user clicks on submit prediction       | `fixture_details`<br />(team names, date, start time)<br />`fixture_state`(play, edit\_prediction)<br />`ll_program_name`<br />`ll_program_id`                                                                                                                                                                      | Tracks number of submissions.                           |

<br />
