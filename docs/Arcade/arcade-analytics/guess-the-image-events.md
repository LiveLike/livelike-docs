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

<br />

<Table align={["left","left","left","left"]}>
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

        _(not included default event properties as outlined[here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_
      </th>

      <th>
        **Event Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **session_start**
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
        **session_stop**
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
        **click_play**
      </td>

      <td>
        When users starts the game by clicking on play button.
      </td>

      <td>
        `total_game_attempts`(number)  
        `pixelation_mode` (boolean)  
        `top_win_streak` (number)  
        `play_streak` (number)  
        `games_played` (number)  
        `games_won` (number)  
        `best_try` (number)
      </td>

      <td>
        Tracks when started playing.
      </td>
    </tr>

    <tr>
      <td>
        **game_completed**
      </td>

      <td>
        When game is over and result screen is displayed.
      </td>

      <td>
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

      <td>
        Captures when the game is over.
      </td>
    </tr>

    <tr>
      <td>
        **click_share**
      </td>

      <td>
        When user clicks on share button after game over (if enabled)
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when user shares the stats.
      </td>
    </tr>

    <tr>
      <td>
        **click_stats**
      </td>

      <td>
        When user clicks on play again button after game over.
      </td>

      <td>
        `top_win_streak`(number)  
        `play_streak` (number)  
        `games_played` (number)  
        `games_won` (number)  
        `best_try` (number)
      </td>

      <td>
        Tracks when user opens stats.
      </td>
    </tr>
  </tbody>
</Table>

<Table align={["center","center","center","center"]}>
  <thead>
    <tr>
      <th>
        **Event Name**
      </th>

      <th>
        **Event Trigger  Condition**
      </th>

      <th>
        **Event Properties**  
        _(not included default event properties as outlined [here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics)  )_
      </th>

      <th>
        **Event Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **session_start**
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
        **session_stop**
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
        **click_play**
      </td>

      <td>
        When users starts the game by clicking on play button.
      </td>

      <td>
        `total_game_attempts`(number)  
        `pixelation_mode` (boolean)  
        `top_win_streak` (number)  
        `play_streak` (number)  
        `games_played` (number)  
        `games_won` (number)  
        `best_try` (number)
      </td>

      <td>
        Tracks when started playing.
      </td>
    </tr>

    <tr>
      <td>
        **game_completed**
      </td>

      <td>
        When game is over and result screen is displayed.
      </td>

      <td>
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

      <td>
        Captures when the game is over.
      </td>
    </tr>

    <tr>
      <td>
        **click_share**
      </td>

      <td>
        When user clicks on share button after game over (if enabled)
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when user shares the stats.
      </td>
    </tr>

    <tr>
      <td>
        **click_stats**
      </td>

      <td>
        When user clicks on play again button after game over.
      </td>

      <td>
        `top_win_streak`(number)  
        `play_streak` (number)  
        `games_played` (number)  
        `games_won` (number)  
        `best_try` (number)
      </td>

      <td>
        Tracks when user opens stats.
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />
