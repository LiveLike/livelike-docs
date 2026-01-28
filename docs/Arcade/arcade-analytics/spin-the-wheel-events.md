---
title: Spin The Wheel Events
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

Below is a list of analytics events triggered in Spin The Wheel, along with their details.

**Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/vitejs-vite-lu5379v7?file=index.html), where event listeners have been integrated and forwarded to Google Analytics (GA).

### **Event List**

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
        **click_spin**
      </td>

      <td>
         When the user clicks on the Spin button
      </td>

      <td>
        `spin_type` (string)
      </td>

      <td>
        Tracks when started playing.
      </td>
    </tr>

    <tr>
      <td>
        **spin_completed**
      </td>

      <td>
         When the wheel stops spinning.
      </td>

      <td>
        `outcome_type` (string)

        `reward_type` (string)
      </td>

      <td>
        This event captures the spin completion
      </td>
    </tr>

    <tr>
      <td>
        **spin_failed**
      </td>

      <td>
        Triggers on failed spin attempts.
      </td>

      <td>
        `error_reason`(string)
      </td>

      <td>
        This event tracks failed spin attempts
      </td>
    </tr>

    <tr>
      <td>
        **game_completed**
      </td>

      <td>
        When the user has no available spins
      </td>

      <td>
        —
      </td>

      <td>
        Captures when the game is over.
      </td>
    </tr>

    <tr>
      <td>
        **visit_page**
      </td>

      <td>
        When the user visits any of the available pages.
      </td>

      <td>
        `page_name` (string)
      </td>

      <td>
        Tracks user visits to any page type
      </td>
    </tr>

    <tr>
      <td>
        **click_sponsor**
      </td>

      <td>
        When user clicks on the sponsor logo (only if clickable)
      </td>

      <td>
        `sponsor_id` (string)
        `sponsor_name` (string)  
        `sponsor_url` (string)
      </td>

      <td>
        Tracks when the user clicks the sponsor logo.
      </td>
    </tr>
  </tbody>
</Table>

<br />
