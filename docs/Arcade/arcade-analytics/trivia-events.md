---
title: ' Trivia Events'
deprecated: false
hidden: false
metadata:
  robots: index
---
Below is a list of analytics events triggered in Trivia, along with their details.

**Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/vitejs-vite-utaxefne?file=index.html), where event listeners have been integrated and forwarded to Google Analytics (GA).

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
        **click_play**
      </td>

      <td style={{ textAlign: "left" }}>
        Triggers when the user starts the game, or when the first question loads if the welcome screen is skipped.
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when started playing.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **game_completed**
      </td>

      <td style={{ textAlign: "left" }}>
        When game is over and result screen is displayed.
      </td>

      <td style={{ textAlign: "left" }}>
        `number_of_questions` (number)
        `win%` (number)
        `is_journey_final_step` (boolean)
      </td>

      <td style={{ textAlign: "left" }}>
        Captures when the game is over.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_share**
      </td>

      <td style={{ textAlign: "left" }}>
        When user clicks on share button after game over (if enabled)
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when user shares the stats.
      </td>
    </tr>
  </tbody>
</Table>
