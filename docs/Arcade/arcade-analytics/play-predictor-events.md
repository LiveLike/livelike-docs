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

<Table>
  <thead>
    <tr>
      <th>
        **Event Name**
      </th>

      <th>
        **Event Trigger Condition**
      </th>

      <th>
        **Event Properties**




        *(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )*
      </th>

      <th>
        **Event Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **session\_start**
      </td>

      <td>
        When the user starts a web session.
      </td>

      <td>
        —
      </td>

      <td>
        Marks the beginning of a session.
      </td>
    </tr>

    <tr>
      <td>
        **session\_stop**
      </td>

      <td>
        When the user exits the web session.
      </td>

      <td>
        `duration` (in seconds)
      </td>

      <td>
        Tracks the total session length.
      </td>
    </tr>

    <tr>
      <td>
        **visit\_page**
      </td>

      <td>
        When the user visits any page.
      </td>

      <td>
        `page_name`\
        (fixtures, predictor\_play, predictor\_edit\_predictions, predictor\_see\_results, predictor\_awaiting\_results, welcome, info, profile, leaderboard)
      </td>

      <td>
        Tracks user navigation between pages.
      </td>
    </tr>

    <tr>
      <td>
        **view\_fixture**
      </td>

      <td>
        When the user views a fixture card.
      </td>

      <td>
        `fixture_details`\
        (team names, date, start time)\
        `fixture_state`\
        (predict\_now, edit\_now, awaiting\_results, see\_results, upcoming/locked)\
        `ll_program_name`\
        `ll_program_id`
      </td>

      <td>
        Captures when users view match fixtures.
      </td>
    </tr>

    <tr>
      <td>
        **interact\_fixture**
      </td>

      <td>
        When the user interacts with a fixture card.
      </td>

      <td>
        `fixture_details`\
        `fixture_state` (play, edit\_prediction, awaiting\_results, locked, see\_results)\
        `ll_program_name`\
        `ll_program_id`
      </td>

      <td>
        Tracks interactions like making or editing predictions.
      </td>
    </tr>

    <tr>
      <td>
        **widget\_viewed**
      </td>

      <td>
        When the user views a question widget.
      </td>

      <td>
        `widget_type` (image prediction, text quiz, text\_prediction\_follow\_up)\
        `widget_state` (active, submitted, expired, result)\
        `question_type` (head-to-head, slider, match score)\
        `question_name`\
        `ll_program_name`\
        `ll_program_id`
      </td>

      <td>
        Tracks when users see a prediction question.
      </td>
    </tr>

    <tr>
      <td>
        **widget\_interacted**
      </td>

      <td>
        When the user submits a response to a widget.
      </td>

      <td>
        `widget_type` (image prediction, text quiz, text\_poll)\
        `widget_state`\
        `question_type`\
        `question_name`\
        `option_index`\
        `option_submitted`\
         `ll_program_name`\
        `ll_program_id`
      </td>

      <td>
        Captures user engagement with prediction widgets.
      </td>
    </tr>

    <tr>
      <td>
        **prediction\_result**
      </td>

      <td>
        When the user views the prediction follow-up widget.
      </td>

      <td>
        `widget_type` (image\_prediction\_follow\_up, text\_prediction\_follow\_up)\
        `question_type`\
        `question_name`\
        `option_submitted`\
        `is_correct` (true/false)\
        `ll_program_name`\
        `ll_program_id`
      </td>

      <td>
        Tracks when users see their prediction results.
      </td>
    </tr>

    <tr>
      <td>
        **nickname\_change**
      </td>

      <td>
        When the user confirms a nickname change.
      </td>

      <td>
        `source_page` (welcome, profile)\
        `old_name`\
        `new_name`
      </td>

      <td>
        Logs nickname changes if applicable.
      </td>
    </tr>

    <tr>
      <td>
        **click\_sponsor**
      </td>

      <td>
        When the user clicks a sponsor logo (if clickable).
      </td>

      <td>
        `sponsor_id`\
        `sponsor_name`\
        `sponsor_url`
      </td>

      <td>
        Tracks sponsor interactions.
      </td>
    </tr>
  </tbody>
</Table>
