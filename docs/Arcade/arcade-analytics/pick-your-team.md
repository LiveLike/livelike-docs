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

[block:parameters]
{
  "data": {
    "h-0": "**Event Name**",
    "h-1": "**Event Trigger Condition**",
    "h-2": "**Event Properties**  \n_(not included default event properties as outlined [here](https://dash.readme.com/project/livelike/v1/docs/arcade-analytics) )_",
    "h-3": "**Event Description**",
    "0-0": "**session_start**",
    "0-1": "When the user starts a web session.",
    "0-2": "—",
    "0-3": "Marks the beginning of a session.",
    "1-0": "**session_stop**",
    "1-1": "When the user exits the web session.",
    "1-2": "`duration` (in seconds)",
    "1-3": "Tracks the total session length.",
    "2-0": "**visit_page**",
    "2-1": "When the user visits any page.",
    "2-2": "`page_name`",
    "2-3": "Tracks user navigation between pages.",
    "3-0": "**start_create_team**",
    "3-1": "When the user first adds a player.",
    "3-2": "`team_name`  (custom name of the team)  \n`choosen_team`  (name of the team ex. Chelsea)  \n`fixture_detail`(details of the fixture)",
    "3-3": "Tracks team creation flow.",
    "4-0": "**team_picked**",
    "4-1": "When the user saves the created team.",
    "4-2": "`team_name`,  \n`choosen_team`,  \n`fixture_detail`,  \n`time_spent` (time to complete team creation from start_create_team to create_team_successfully),  \n`selected_players` (list of selected players),  \n`is_journey_final_step` (boolean)",
    "4-3": "Captures when user has finalized the team.",
    "5-0": "**click_share**",
    "5-1": "When the user clicks on share button after game over.",
    "5-2": "—",
    "5-3": "Tracks sharing of created teams.",
    "6-0": "**click_download**",
    "6-1": "When the user clicks on download button after game over.",
    "6-2": "—",
    "6-3": "Tracks when users downloads final team.",
    "7-0": "**click_edit**",
    "7-1": "When the user clicks on edit button after game over.",
    "7-2": "—",
    "7-3": "Tracks when users edit previously created teams."
  },
  "cols": 4,
  "rows": 8,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]