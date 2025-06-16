---
title: Trivia CMS Guide
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
The Trivia Minigame is a customizable quiz platform offering three distinct gameplay configurations to suit different engagement needs. It features:

1. **Timed quizzes with manual submission**, letting players review answers before submitting while maintaining competitive time pressure
2. **Untimed quizzes with submission control**, ideal for educational and casual settings where thoughtful responses matter more than speed. 
3. **Timer-based automatic submission**, perfect for driving competition. 

The platform includes comprehensive customization options for scoring, result displays, and social features like leaderboards and rewards. Game administrators can maintain brand consistency through theme customization and control game availability through flexible scheduling options. Lets get started with Trivia setup 

Trivia is available in the experiences list.

<Image align="center" width="600px" src="https://files.readme.io/3d935f860b3ba937e8ec6c0be1122a48a3ebd7b57964fa6aea536eddabd2624e-Screenshot_2024-12-18_at_15.36.32.png" />

To begin, either select an existing game or click "Create New" to start fresh. The setup process consists of 6 key steps.

<Image align="center" src="https://files.readme.io/af79ff404557181799a6751a06fbd772b93f2d177f1bae262c208deaf5927682-ezgif-2-aa0c6889bd.gif" />

1. **Welcome**
   1. This is the initial configuration page for Trivia games where you set up the player's first interaction with the game.
   2. It focuses on providing clear instructions and game structure information before players begin the actual trivia experience.
   3. This page is skippable. If skipped, user will directly land on the Trivia Questions.

<Image align="center" width="600px" src="https://files.readme.io/92ba829a74e58d542d3af22acbeff704d758292d2fc293af743f7493f9cd0425-Screenshot_2024-12-18_at_15.08.38.png" />

2. **Trivia Question setup**
   1. **Add questions button:**
      1. Create questions through three methods:
         1. CSV UPLOAD: Upload questions via CSV file
         2. Manual: Add questions individually
         3. GenAI: Generate questions using AI 
   2. **Timer Settings** 
      1. **Timer Options:**
         1. None: No time limit
         2. Global: Same time for all questions
         3. Individual: Custom time per question
      2. **Timer type:** Select countdown style
         1. Countdown 
         2. Progress bar 

<Image align="center" src="https://files.readme.io/756fcfd1b67838f6740216262167133ab9d4c37d9d6be1b08f4ddeabef872e79-sss.gif" />

***

<br />

**Using the timer and submission control, below types of Trivia can be configured**

**Timer + Submission control button**

1. Answer Record: On click of the Submit button. Before clicking the submit button, user has chance to change the selected options.
2. Answer Display: Feedback is shown after submission
3. Next Question: Loads after the timer is over.
4. Use Case: Standard trivia with time pressure, allowing users control over submission.
5. Benefits: Balances time management with user control.

**No Timer + Submission control button (Next)**

1. Answer Record: On click of the Submit button. Before clicking the submit button, user has chance to change the selected options.
2. Answer Display: Feedback is shown after submission.
3. Next Question: Loads after the user clicks Submit/Next.
4. Use Case: Casual or educational trivia sessions without time pressure.
5. Benefits: Users can focus on answering thoughtfully, without rushing.

**Timer + No Submission control**

1. Answer Record: Tapping on an option automatically records the answer without an option to change 
2. the selected answer.
3. Answer Display: Feedback is shown after the timer expires.
4. Next Question: Loads after the timer is over with a short delay
5. Use Case: Best for Live Trivia, ensuring real-time responses from all players simultaneously.

***

<br />

3. **Result screen**
   1. The Result Screen setup lets you configure how players see their trivia game outcomes, with options for Single or Score based display. 
   2. For Score based results, you can customize messages for different performance levels (90%+, 50-90%, and below 50%), each with encouraging feedback. 
   3. Additional toggles allow for showing points, enabling result sharing, and letting players review their questions after completion. *(sharing is currently in beta and dependent on browser support)*

<Image align="center" width="600px" src="https://files.readme.io/d313034706fea03afd9f00831a6c9e737b01506ea38af7459c78d2576056255f-Screenshot_2024-12-18_at_15.28.16.png" />

4. **Social features**
   1. The Social Features page focuses on Rewards & Leaderboards configuration for the Trivia game. It includes two primary dropdown selection fields: "Select reward table" for setting up player rewards and "Select leaderboard" for configuring the game's leaderboard system.
   2. To link these, its important that the Rewards and Leaderboard are pre-created in the core CMS.

<Image align="center" width="600px" src="https://files.readme.io/78006b4676347b5652fcaf08f54066e966f98ba5a299ed40dca957d804ec9d91-Screenshot_2024-12-18_at_15.29.01.png" />

5. **Theme setup**
   1. You can customize the visual branding and theme elements of your game.
   2. This is part of the game's customization process, allowing you to maintain brand consistency and create a unique visual identity for your Trivia implementation. 
   3. The theme setup ensures your game matches your brand's visual guidelines and style requirements.
   4. **Please Note:**
      1. The structured of the Trivia will remain the same. 
      2. Colors or Background Images on Welcome Screen, Question Page, Results Page can be changed. 
      3. Text copies can be changed only on Welcome page and End result screen. 
      4. Positioning, adding and resizing of components cannot be done. 
      5. Font: Configurable in the Theme setup.  
      6. Background image: Recommended size 1080x1920 , max size 1mb 

<Image align="center" src="https://files.readme.io/5a529ce9b0dcb435a91360bfc45580d225f3eceac0a7b13a2617ed74959eb83c-sdsd.gif" />

6. **Schedule**
   1. The Schedule configuration page offers two timing options for your trivia game: "Publish now" for immediate release or "Schedule" for setting a future publication date and time. 
   2. When scheduling, you can specify the exact date and time (shown in the format DD/MM/YYYY, HH:MM:SS am/pm) for when the game should become available to players. 
   3. This timing control helps coordinate game releases with specific events or optimal player engagement periods.
   4. If multiple Trivia are created, the schedule of the upcoming Trivia will be visible on result screen of the Trivia which is currently Live. 

<Image align="center" width="600px" src="https://files.readme.io/7ec59110d0ad452867cc2b901a67479400f1773ed15060bebbf190c8dc016a3f-Screenshot_2024-12-18_at_15.38.17.png" />
