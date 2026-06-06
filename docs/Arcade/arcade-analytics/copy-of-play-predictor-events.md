---
title: Play Predictor +  Events
deprecated: false
hidden: true
metadata:
  robots: index
---
Below is a list of analytics events triggered in Play Predictor+, along with their details.

> **Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/react-vxwfaksw?file=analytics-service.js), where event listeners have been integrated and forwarded to Google Analytics (GA).

### **Event List**

| **Event Name**         | **Event Trigger Condition**                     | **Event Properties**_(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_                                                                  | **Event Description**                               |
| :--------------------- | :---------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------- |
| **session\_start**     | When the user starts a web session.             | —                                                                                                                                                                                                                    | Marks the beginning of a session.                   |
| **session\_stop**      | When the user exits the web session.            | `duration` (in seconds)                                                                                                                                                                                              | Tracks the total session length.                    |
| **visit\_page**        | When the user visits any page.                  | `page_name`<br />(upcoming, results, leaderboard)                                                                                                                                                                    | Tracks user navigation between pages.               |
| **view\_fixture**      | When the user views a fixture card.             | `fixture_details,`<br />`fixture_state`<br />(predict\_now, edit\_now, awaiting\_results, view\_results, locked),<br />`ll_program_name,`<br />`ll_program_id`                                                       | Captures when users view match fixtures.            |
| **widget\_interacted** | When the user submits a response to a question. | `widget_type` (image prediction, text quiz, text\_poll),<br />`widget_state,`<br />`question_type,`<br />`question_name,`<br />`option_index,`<br />`option_submitted,`<br />`ll_program_name,`<br />`ll_program_id` | Captures user engagement with prediction questions. |
| **nickname\_change**   | When the user confirms a nickname change.       | `source_page` (welcome, profile);<br />`old_name;`<br />`new_name`                                                                                                                                                   | Logs nickname changes if applicable.                |
| **game\_completed**    | Triggers when user clicks on submit prediction  | `fixture_details`<br />(team names, date, start time);<br />`fixture_state`(play, edit\_prediction),<br />`ll_program_name,`<br />`ll_program_id,`<br />`total_questions`                                            | Tracks number of submissions.                       |

<br />
