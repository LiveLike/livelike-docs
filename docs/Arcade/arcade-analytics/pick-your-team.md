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

| **Event Name**           | **Event Trigger Condition**                              | **Event Properties**_(not included default event properties as outlined [here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_                                                                                                                                                                                                                 | **Event Description**                            |
| :----------------------- | :------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------- |
| **session\_start**       | When the user starts a web session.                      | —                                                                                                                                                                                                                                                                                                                                                                    | Marks the beginning of a session.                |
| **session\_stop**        | When the user exits the web session.                     | `duration` (in seconds)                                                                                                                                                                                                                                                                                                                                              | Tracks the total session length.                 |
| **visit\_page**          | When the user visits any page.                           | `page_name`(welcome,<br />team\_selection,<br />team\_fixture,<br />playground)                                                                                                                                                                                                                                                                                      | Tracks user navigation between pages.            |
| **start\_create\_team**  | When the user first adds a player.                       | `team_name`  (custom name of the team),<br />`choosen_team`  (name of the team ex. Chelsea),<br />`fixture_detail`(details of the fixture),<br />`fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id`                                                                                                                            | Tracks team creation flow.                       |
| **team\_player\_picked** | When a team is saved by the user.                        | `position,player_name,`<br />`fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id`                                                                                                                                                                                                                                                | Tracks the selected players' details.            |
| **game\_completed**      | When the user saves the created team.                    | `team_name`,<br />`choosen_team`,<br />`fixture_detail`,<br />`time_spent` (time to complete team creation from start\_create\_team to create\_team\_successfully),<br />`selected_players` (list of selected players),<br />`is_journey_final_step` (boolean),<br />`fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id,`<br /> | Captures when user has finalized the team.       |
| **click\_share**         | When the user clicks on share button after game over.    | `fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id`                                                                                                                                                                                                                                                                             | Tracks sharing of created teams.                 |
| **click\_download**      | When the user clicks on download button after game over. | `fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id`                                                                                                                                                                                                                                                                             | Tracks when users downloads final team.          |
| **click\_edit**          | When the user clicks on edit button after game over.     | `fixture_name,`<br />`fixture_id,`<br />`tournament_name,`<br />`tournament_calendar_id`                                                                                                                                                                                                                                                                             | Tracks when users edit previously created teams. |

<br />
