---
title: Guess The Image Events
deprecated: false
hidden: false
metadata:
  robots: index
---
Below is a list of analytics events triggered in Guess The Image, along with their details.

**Note:** For a practical implementation reference, explore our <Anchor label="demo" target="_blank" href="https://stackblitz.com/edit/vitejs-vite-7wiwh6jm?file=index.html">demo</Anchor>, where event listeners have been integrated and forwarded to Google Analytics (GA).

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

        _(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics)  )_
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
        When users starts the game by clicking on play button.
      </td>

      <td style={{ textAlign: "left" }}>
        `total_game_attempts` (number)
        `pixelation_mode` (boolean)

        `top_win_streak` (number)
        `play_streak` (number)
        `games_played` (number)
        `games_won` (number)
        `best_try` (number)
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
        `total_game_attempts` (number)
        `pixelation_mode` (boolean)
        `top_win_streak` (number)
        `play_streak` (number)
        `games_played` (number)
        `games_won` (number)
        `best_try` (number)
        `guess_result` (string)
        `attempt_number` (number)
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

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_stats**
      </td>

      <td style={{ textAlign: "left" }}>
        When user clicks on play again button after game over.
      </td>

      <td style={{ textAlign: "left" }}>
        `top_win_streak` (number)
        `play_streak` (number)
        `games_played` (number)
        `games_won` (number)
        `best_try` (number)
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when user opens stats.
      </td>
    </tr>
  </tbody>
</Table>

<br />
