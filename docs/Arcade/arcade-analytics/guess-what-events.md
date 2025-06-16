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
    "1-1": "When the user exits the web session. ",
    "1-2": "`duration` (in seconds)",
    "1-3": "Tracks the total session length.",
    "2-0": "**click_play**",
    "2-1": "When users starts the game by clicking on play button.",
    "2-2": "—",
    "2-3": "Tracks when started playing.",
    "3-0": "**game_completed**",
    "3-1": "When game is over and result screen is displayed.",
    "3-2": "`give_up` (boolean)  \n`is_winner` (boolean)  \n`number_of_questions` (number)  \n`tags` (string)  \n`accuracy` (number)  \n`is_journey_final_step` (boolean)  \n`hints_used` (boolean)",
    "3-3": "Captures when the game is over.",
    "4-0": "**click_share**",
    "4-1": "When user clicks on share button after game over (if enabled)",
    "4-2": "—",
    "4-3": "Tracks when user shares the stats.",
    "5-0": "**click_play_again**",
    "5-1": "When user clicks on play again button after game over.",
    "5-2": "—",
    "5-3": "Tracks when attempts play again.",
    "6-0": "**click_play_more**",
    "6-1": "When user clicks on play more button after game over.",
    "6-2": "—",
    "6-3": "Tracks when user explores play more."
  },
  "cols": 4,
  "rows": 7,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]