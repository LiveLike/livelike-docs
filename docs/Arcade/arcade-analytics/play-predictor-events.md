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

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        **Event Name**
      </th>

      <th style={{ textAlign: "left" }}>
        **Event Trigger Condition**
      </th>

      <th style={{ textAlign: "left" }}>
        **Event Properties**

        _(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_
      </th>

      <th style={{ textAlign: "left" }}>
        **Event Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        **session_start**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user starts a web session.
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Marks the beginning of a session.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **session_stop**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user exits the web session.
      </td>

      <td style={{ textAlign: "left" }}>
        `duration` (in seconds)
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks the total session length.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **visit_page**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user visits any page.
      </td>

      <td style={{ textAlign: "left" }}>
        `page_name`  
        (fixtures, predictor_play, predictor_edit_predictions, predictor_see_results, predictor_awaiting_results, welcome, info, profile, leaderboard)
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks user navigation between pages.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **view_fixture**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user views a fixture card.
      </td>

      <td style={{ textAlign: "left" }}>
        `fixture_details`  
        (team names, date, start time)  
        `fixture_state`  
        (predict_now, edit_now, awaiting_results, see_results, upcoming/locked)  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Captures when users view match fixtures.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **interact_fixture**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user interacts with a fixture card.
      </td>

      <td style={{ textAlign: "left" }}>
        `fixture_details`  
        `fixture_state` (play, edit_prediction, awaiting_results, locked, see_results)  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks interactions like making or editing predictions.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **widget_viewed**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user views a question widget.
      </td>

      <td style={{ textAlign: "left" }}>
        `widget_type` (image prediction, text quiz, text_prediction_follow_up)  
        `widget_state` (active, submitted, expired, result)  
        `question_type` (head-to-head, slider, match score)  
        `question_name`  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when users see a prediction question.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **widget_interacted**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user submits a response to a widget.
      </td>

      <td style={{ textAlign: "left" }}>
        `widget_type` (image prediction, text quiz, text_poll)  
        `widget_state`  
        `question_type`  
        `question_name`  
        `option_index`  
        `option_submitted`  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Captures user engagement with prediction widgets.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **prediction_result**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user views the prediction follow-up widget.
      </td>

      <td style={{ textAlign: "left" }}>
        `widget_type` (image_prediction_follow_up, text_prediction_follow_up)  
        `question_type`  
        `question_name`  
        `option_submitted`  
        `is_correct` (true/false)  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when users see their prediction results.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **nickname_change**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user confirms a nickname change.
      </td>

      <td style={{ textAlign: "left" }}>
        `source_page` (welcome, profile)  
        `old_name`  
        `new_name`
      </td>

      <td style={{ textAlign: "left" }}>
        Logs nickname changes if applicable.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_sponsor**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user clicks a sponsor logo (if clickable).
      </td>

      <td style={{ textAlign: "left" }}>
        `sponsor_id`  
        `sponsor_name`  
        `sponsor_url`
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks sponsor interactions.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **game_completed**
      </td>

      <td style={{ textAlign: "left" }}>
        Triggers when user clicks on submit prediction
      </td>

      <td style={{ textAlign: "left" }}>
        `fixture_details`  
        (team names, date, start time)  
        `ll_program_name`  
        `ll_program_id`
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks number of submissions. 
      </td>
    </tr>
  </tbody>
</Table>

<br />
