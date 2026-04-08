---
title: Sweepstakes Events
deprecated: false
hidden: false
metadata:
  robots: index
---
Below is a list of analytics events triggered in Sweepstakes, along with their details.

**Note:** For a practical implementation reference, explore our , where event listeners have been integrated and forwarded to Google Analytics (GA).

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
        **view_sweepstake**
      </td>

      <td style={{ textAlign: "left" }}>
        Triggers when user views the sweepstake details or landing screen
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Track user viewing sweepstake details or landing screen
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_join_sweepstake**
      </td>

      <td style={{ textAlign: "left" }}>
        Fires when the user taps or clicks the Join/Participate button on any screen, indicating the initiation of participation.
      </td>

      <td style={{ textAlign: "left" }}>
        `source` (string)
      </td>

      <td style={{ textAlign: "left" }}>
        Triggered when a user clicks on the Join or Participate button to start participation in the sweepstakes.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **extra_entry_earned**
      </td>

      <td style={{ textAlign: "left" }}>
        Fires when a user successfully earns an extra entry after completing a qualifying action (e.g., email submission, referral, or similar)
      </td>

      <td style={{ textAlign: "left" }}>
        `source` (string)
      </td>

      <td style={{ textAlign: "left" }}>
        Triggered when a user earns an additional entry through actions such as email submission, referrals, etc
      </td>
    </tr>
  </tbody>
</Table>
