---
title: Pick Your Team Events
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
Below is a list of analytics events triggered in Pick Your Team, along with their details.

> **Note:** For a practical implementation reference, explore our [demo](https://stackblitz.com/edit/vitejs-vite-g5txt3ae?file=package.json), where event listeners have been integrated and forwarded to Google Analytics (GA).

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
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks user navigation between pages.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **start_create_team**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user first adds a player.
      </td>

      <td style={{ textAlign: "left" }}>
        `team_name`  (custom name of the team)  
        `choosen_team`  (name of the team ex. Chelsea)  
        `fixture_detail`(details of the fixture)
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks team creation flow.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **game_completed**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user saves the created team.
      </td>

      <td style={{ textAlign: "left" }}>
        `team_name`,  
        `choosen_team`,  
        `fixture_detail`,  
        `time_spent` (time to complete team creation from start_create_team to create_team_successfully),  
        `selected_players` (list of selected players),  
        `is_journey_final_step` (boolean)
      </td>

      <td style={{ textAlign: "left" }}>
        Captures when user has finalized the team.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_share**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user clicks on share button after game over.
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks sharing of created teams.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_download**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user clicks on download button after game over.
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when users downloads final team.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        **click_edit**
      </td>

      <td style={{ textAlign: "left" }}>
        When the user clicks on edit button after game over.
      </td>

      <td style={{ textAlign: "left" }}>
        —
      </td>

      <td style={{ textAlign: "left" }}>
        Tracks when users edit previously created teams.
      </td>
    </tr>
  </tbody>
</Table>
