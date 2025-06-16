---
title: Guess What Events
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
Below is a list of analytics events triggered in Guess What, along with their details.  

**Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/vitejs-vite-orguuifq), where event listeners have been integrated and forwarded to Google Analytics (GA).  

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
        **click\_play**
      </td>

      <td>
        When users starts the game by clicking on play button.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when started playing.
      </td>
    </tr>

    <tr>
      <td>
        **game\_completed**
      </td>

      <td>
        When game is over and result screen is displayed.
      </td>

      <td>
        `give_up` (boolean)\
        `is_winner` (boolean)\
        `number_of_questions` (number)\
        `tags` (string)\
        `accuracy` (number)\
        `is_journey_final_step` (boolean)\
        `hints_used` (boolean)
      </td>

      <td>
        Captures when the game is over.
      </td>
    </tr>

    <tr>
      <td>
        **click\_share**
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
        **click\_play\_again**
      </td>

      <td>
        When user clicks on play again button after game over.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when attempts play again.
      </td>
    </tr>

    <tr>
      <td>
        **click\_play\_more**
      </td>

      <td>
        When user clicks on play more button after game over.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when user explores play more.
      </td>
    </tr>
  </tbody>
</Table>
