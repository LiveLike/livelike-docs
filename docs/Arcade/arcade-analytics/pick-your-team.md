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
        `page_name`
      </td>

      <td>
        Tracks user navigation between pages.
      </td>
    </tr>

    <tr>
      <td>
        **start\_create\_team**
      </td>

      <td>
        When the user first adds a player.
      </td>

      <td>
        `team_name`  (custom name of the team)\
        `choosen_team`  (name of the team ex. Chelsea)\
        `fixture_detail`(details of the fixture)
      </td>

      <td>
        Tracks team creation flow.
      </td>
    </tr>

    <tr>
      <td>
        **team\_picked**
      </td>

      <td>
        When the user saves the created team.
      </td>

      <td>
        `team_name`,\
        `choosen_team`,\
        `fixture_detail`,\
        `time_spent` (time to complete team creation from start\_create\_team to create\_team\_successfully),\
        `selected_players` (list of selected players),\
        `is_journey_final_step` (boolean)
      </td>

      <td>
        Captures when user has finalized the team.
      </td>
    </tr>

    <tr>
      <td>
        **click\_share**
      </td>

      <td>
        When the user clicks on share button after game over.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks sharing of created teams.
      </td>
    </tr>

    <tr>
      <td>
        **click\_download**
      </td>

      <td>
        When the user clicks on download button after game over.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when users downloads final team.
      </td>
    </tr>

    <tr>
      <td>
        **click\_edit**
      </td>

      <td>
        When the user clicks on edit button after game over.
      </td>

      <td>
        —
      </td>

      <td>
        Tracks when users edit previously created teams.
      </td>
    </tr>
  </tbody>
</Table>
