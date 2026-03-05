---
title: Guess The Image CMS Guide
deprecated: false
hidden: false
metadata:
  robots: index
---
Guess the Image minigame challenges users to identify an image using a limited number of attempts. Images can optionally appear pixelated to increase the difficulty of the challenge. Players attempt to guess the correct answer before exhausting their allowed attempts.

Producers can configure the game schedule, rules, attempts, themes, and localization through the MiniGames CMS.

**CMS Setup**

GTI (Guess The Image) is available in the experiences list.

![](https://files.readme.io/ade6c984b8221e07c7ff6102690df38bce0dfd3b41d0d9c76cab21144288597b-image.png)

To begin, either select an existing game or click "Create New" to start fresh. The setup process consists of 6 key steps.

![](https://files.readme.io/ca2811c9bf3bd98cd8133a96f92eda233526fdf07cf8ccbd4a8dc5cfec7c5da9-image.png)

<br />

1. **Game Settings**
   1. Game Timezone: Set primary timezone (e.g., Asia/Kolkata) based on target audience
   2. Word Reset Time: Configure daily refresh time in 24-hour format (e.g., 07:00)
   3. Game Start Date: Define launch date (e.g., December 17th, 2024)  
      Tip: Align launch with marketing activities

<Image align="center" width="650px" src="https://files.readme.io/3658431b18236b9aab0d32cbb56d0fef191359be41f47a1c489bf066409e4f59-Screenshot_2024-12-18_at_10.56.09.png" />

<br />

2. **Game Copies** Configure game text elements:
   1. Welcome screen with custom greeting and start button
   2. End screen with closing message
   3. Result screen with two display types: Single/Score Based

<Image align="center" src="https://files.readme.io/f0d1224c5d53067e314e8e7b33aba769bb095d3b0abdaed4c9d8356038518139-ScreenRecording2024-12-18at10.59.15-ezgif.com-video-to-gif-converter.gif" />

3. **Word Database**
   1. You can set up target words for each date, with support for word lengths ranging from 5 to 10 letters.
   2. The platform provides fields to enter different word lengths per day, helping you create varied and engaging gameplay.
   3. By default, we provide a database of per-configured words for 100days.
   4. Currently, manual word entry is the supported method for adding words to the database. You can add or delete the rows and columns to manage the words.
   5. **Upload allowed word:** If your game includes words not found in the standard dictionary, you can upload a CSV file containing custom words that match your theme. These will be recognized as valid entries during gameplay else the words entered if not part of the dictionary will throw an error.
   6. **New Updates** allows you to toggle off support for Dictionary words or define the cadence of when the word should go live, either daily, weekly or custom. Just click on the date and pick the date you want the word to go-live on.

<Image align="center" src="https://files.readme.io/ea25ca9686b59ac764e6db480e680566118ab2cd093f5ea91a0035a676c85514-ezgif-2-9b6a19bee6.gif" />

4. **Theme Setup**
   1. In this step, you can customize the visual branding and theme elements of your game.
   2. This is part of the game's customization process, allowing you to maintain brand consistency and create a unique visual identity for your GTW implementation. The theme setup ensures your game matches your brand's visual guidelines and style requirements.
   3. **Please note:**
      1. The structure of the game stays the same. Poistioning, adding and resizing of components cannot be done
      2. Only colors/background images and text copies can be customised
      3. Brand Logo -  Max size: 42x300 pixels
      4. Game Font: Applied to all text except letters inputed in the Grid.
      5. Grid Font: Applied to only Letters in the Grid.
      6. Game logo: Max size: 42x300 pixels
      7. Sponsor Logo: Max size: 42x300 pixels
      8. Background image: Recommended size 1080x1920 , max size 1mb

<Image align="center" src="https://files.readme.io/7068cc08423bfee8b8806475ddc8be970380b516e77f854739ff54ee5b05cd3c-ezgif-5-70918d4920.gif" />

5. **Social features**
   1. The section includes toggles for showing user stats and enabling stat sharing capabilities.
   2. Players can customize a share message (defaulted to "Join me in today's word puzzle") to invite others. The Deeplink feature allows configuration of deep linking functionality, along with a countdown toggle that display a countdown when today's game ends but the new game hasn't started yet,indicating when the next game day begins.
   3. Count Down features when enabled displays a countdown when today's game ends but the new game hasn't started yet, indicating when the next game day begins.

<Image align="center" src="https://files.readme.io/f134fd99d7fecb15e2804be8fa608b733bf4dce6d461c0b9cdfe1446bcc1a754-Screenshot_2025-08-13_at_10.04.57.png" />

6. **Live Game Manager**
   1. This section provides real-time management capabilities for your GTW game.
   2. This interface includes a "Publish Game" button for launching your game and displays a word timeline.
