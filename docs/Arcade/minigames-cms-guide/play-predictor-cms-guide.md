---
title: Play Predictor CMS Guide
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
The Play Predictor MiniGame is a customisable prediction game that can enhance fan engagement by allowing your users to predict outcomes in live or scheduled events, accumulate points, and compete on leaderboards.

You can have complete control to create and run multiple Play Predictors independently, through a dedicated CMS that lets you -

- Choose between showing all match fixtures in advance or just one at a time
- Add and preview all match details and necessary assets with ease using a CSV
- Use social features like leaderboards and points to make the game competitive
- Introduce variations using a multitude of question types to drive more engagement
- Showcase a sponsor for the game, if you have one
- Customize every aspect of the UI to suit your brand guidelines
- Resolve predictions all at once or individually, both in real-time or post-match

**Let’s get started with the Predictor setup in the CMS!**

***

Predictor is available in the “All Games” section. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bc71a461294a71f109ee90a1c2725dd1e69b43ed57063d8f16a1ea40d58440b2-Screenshot_2025-03-28_at_17.07.49.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


To begin, either select an existing game or click "Create New" to start fresh. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a92a4e1091924ed50b9f1f2837abed828cd728d5d55ea083d8ac4c0a1986141f-unnamed.gif",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The setup process consists of 7 simple steps:

1. **Welcome & Information Screen**

   1. This is the initial configuration step for the Predictor where you can set up players’ first interaction with the game.
   2. If “Welcome & Nickname Selection” screen is enabled, users will get access to “Welcome” and “User Profile” pages where they can -
   3. Pick a nickname/alias of their choice, updating the one randomly assigned to them by LiveLike on first their launch.
   4. Change their nickname at any later point.
   5. If “Information & Rules Screen” is enabled, users will get access to an “Info” page where they are able to see game rules or any other key information.
   6. This step is optional, so can be skipped based on your use case.

   [block:image]{"images":[{"image":["https://files.readme.io/35449c064c812ddba35cc53279f57db6c6b4e4e76c0b0366aae193bb51f38adb-Screenshot_2025-03-28_at_17.11.42.png","",""],"align":"center"}]}[/block]
2. **Fixtures**

   1. At this step, you can choose to show all fixtures from a tournament or only one match at a time.
   2. If “All” is selected, users can view all fixture cards, but you can - 
      1. Configure showing grouped fixtures such as Week 1, Week 2, Quarter Finals, Semi-Finals, Finals, etc.
      2. Restrict user-interaction to select fixtures by adjusting “Fixture Interactivity” to Daily, Weekly, Monthly, etc.
   3. If “One At A Time” is selected, users will only see one game, either most recently completed or next upcoming, at a time, but you can configure 
      1. How long before the match start time does the corresponding predictor go live?
      2. How long after the match start time does the corresponding predictor results are visible to users?
   4. In case of an overlap between “Prediction Starts At” and “Show Results Until” time, the former will take precedence, so users can make predictions for the upcoming match.
   5. Please note that all time calculations are based on match start time.
   6. This is also an optional step, so can be skipped based on your use case.

   [block:image]{"images":[{"image":["https://files.readme.io/3fd3f46d6312d65af42ec3cd461b8c39f4457d75859eb482f2a9ffbfe5c281ca-Screenshot_2025-03-28_at_18.24.15.png",null,""],"align":"center"}]}[/block]
3. **Sports & Tournament**

   1. This is a key step where you can add match information and image assets for the Predictor.  
      It is the source of any and all data points needed to set up the game. For now, only CSV upload is supported.
   2. You can download the attached sample CSV files for fixtures and image assets, add all relevant information and links, and upload it.  
      Please adhere to the format of both CSVs to ensure the data is captured correctly.  
      We strongly recommend validating the information on this page itself, under the “Preview” section.  
      This step is mandatory.

   [block:image]{"images":[{"image":["https://files.readme.io/096d46c16e341f04d5a669621f122ee0329717445a11c1455c9fbd55268c0606-Screenshot_2025-03-28_at_18.24.45.png",null,""],"align":"center"}]}[/block]
4. **Rewards & Leaderboards**

   1. This step lets you include social / community features to the Predictor.
   2. You can choose to show or hide feedback to users on individual questions once prediction is resolved.

      [block:image]{"images":[{"image":["https://files.readme.io/ce0f2afe7c2016067d45ff41ad31126f8a9f29e5dba3144330d503222fa266fb-Screenshot_2025-03-28_at_18.25.06.png",null,""],"align":"center"}]}[/block]
   3. Selecting a reward item is mandatory - you can either pick it from the dropdown list of available reward items or create a new one.

      [block:image]{"images":[{"image":["https://files.readme.io/1e38e0e70f94c87b8f938549d071ee58ef9219eddbb18596d44ae479a1831557-Screen_Recording_2025-03-05_at_9.03.44_PM.gif",null,""],"align":"center"}]}[/block]
   4. You can also enable leaderboards and select one or more types between a season/tournament-level, round-level, match-level - it will auto-create those leaderboards.
   5. You can also link the current Play Predictor’s leaderboards to an existing leaderboard from any other of your experiences that LiveLike may be powering.
   6. Having a leaderboard is optional.
5. **Create Questions**

   1. At this step, you can set up questions for the predictor game as well as set up the scoring system.
   2. You can either have the same points for all prediction questions (Global) or each question to have a different score based on complexity (Individual).

      [block:image]{"images":[{"image":["https://files.readme.io/c745960770f542a5564cf008cd906043cd2161a59a6eb6da55eee63f53191ed3-Screenshot_2025-03-28_at_18.21.59.png",null,""],"align":"center"}]}[/block]
   3. For setting up prediction questions, can either update the pre-added sample questions for each question type or add new ones altogether.
   4. Please note that the questions will be visible to users in the exact order as shown in the CMS, but you can reorder questions from the 3-dot menu next to each question.
   5. Questions can be configured to show option choices either between teams or between individual players.

      [block:image]{"images":[{"image":["https://files.readme.io/082606f512c365a038f6d8d2d2920b5900e1f30c93d77af07fd17a6085a57841-Screen_Recording_2025-03-05_at_9.05.51_PM.gif",null,""],"align":"center"}]}[/block]
   6. You can also enable “Participation Score” to reward points to users who attempted but ended up making incorrect predictions - this is optional, so can be skipped based on your use case. Please note that this score is assigned globally to all questions, if enabled.
6. **Sponsor**

   1. At this step, you can add any sponsor for the game.
   2. You can also include a URL while adding a sponsor to redirect users to a sponsored link, if required.
   3. The sponsor you have added will be visible on this page.
   4. Please note that you can only have one sponsor per Predictor, which will be visible throughout all matches that are part of that predictor.
   5. You can however, switch sponsors at any point that will be effective from upcoming matches.

      [block:image]{"images":[{"image":["https://files.readme.io/3d2da0d46bbb497f59268883ce4895c076d57247db2dc858c14e0cb46a29a83b-Screenshot_2025-03-28_at_18.21.29.png",null,""],"align":"center"}]}[/block]
7. **Theme & Branding**

   1. At this step, you can customize the visual branding and theme elements of your game.
   2. This is part of the game's customization process, allowing you to maintain brand consistency and create a unique visual identity for your Play Predictor implementation.
   3. The theme setup ensures your game matches your brand's visual guidelines and style requirements.
   4. You will be able to create new themes or use any existing themes from the dropdown list.
   5. You can also download themes created during testing and upload those files in production to quickly set up the production environment.
   6. Please Note:

      1. The structure of Play Predictor will remain the same.
      2. Font family, color, background images, or logos can be customized.
      3. Copies can be changed for CTA buttons and headers, wherever specified.
      4. Positioning, adding and resizing of components cannot be done.
      5. Image size and dimensions, wherever applicable, have been specified in the CMS. In general, please upload images of 1MB or less file size.

         [block:image]{"images":[{"image":["https://files.readme.io/9c8caa09541aed82b54935a881ccc57122f40b15df695a3c0d68a155055a3ba4-Screen_Recording_2025-03-05_at_9.30.23_PM.gif",null,""],"align":"center"}]}[/block]

Once you set up a Predictor game, you will be able to see it in the “Play Predictor” page. You can see details like when was it created or updated and by who, along with the number of matches it has and its status. All “Completed” predictors can be found under the “History” tab. Please note that a “Completed” predictor signifies that all of its matches have been played.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6f503523d3dbe518a02f46ee273243d7b8049616f04929cdd1b6dabc6356cfcb-Screenshot_2025-03-28_at_18.17.13.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


From here, you can click on the predictor to view all matches within it. You can also make desired modifications by clicking on “Edit”. Please note that editing a predictor game will only impact its upcoming matches. While editable, we recommend keeping the scoring system unchanged throughout the course of the predictor to ensure level-playing field for users who started playing before or after the modifications made to the game.

Once you are in the match-view of a predictor, you can access the Control Panel of an ongoing or completed match to start resolving the predictions. The Control Panel is intuitively designed to let you easily publish the results of predictions as and when you want. It provides you the flexibility to publish the results both in bulk or individually, in real time or post-match.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/82a338d2a5a13ce25b7813ddbcae6ee9187669720395846418e58cb4ca4b67df-Screen_Recording_2025-03-05_at_9.54.23_PM.gif",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]