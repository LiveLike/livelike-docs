---
title: Guess The Image CMS Guide
deprecated: false
hidden: false
metadata:
  robots: index
---
Guess The Image minigame challenges users to identify an image using a limited number of attempts. Images can optionally appear pixelated to increase the difficulty of the challenge. Players attempt to guess the correct answer before exhausting their allowed attempts.

Producers can configure the game schedule, rules, attempts, themes, and localization through the MiniGames CMS.

**CMS Setup**

GTI (Guess The Image) is available in the experiences list.

![](https://files.readme.io/ade6c984b8221e07c7ff6102690df38bce0dfd3b41d0d9c76cab21144288597b-image.png)

To begin, either select an existing game or click "Create New" to start fresh. The setup process consists of 8 key steps.

![](https://files.readme.io/ca2811c9bf3bd98cd8133a96f92eda233526fdf07cf8ccbd4a8dc5cfec7c5da9-image.png)

<br />

1. **Game Settings**
   1. The Game Settings section defines when the game starts and when new images reset.
      1. Game Start Date: Defines the date when the game becomes active and available to players.
      2. Word Reset Time (UTC): Defines the time when the next scheduled image becomes active.
      3. The reset time determines when a new image from the database will be displayed to users.
      4. Summary: The CMS displays a summary showing the reset time converted into the Producer’s local timezone.

         Example:

         UTC Time: 12:00 AM
         Local Time: 05:30 AM IST

![](https://files.readme.io/da4241caa9585352cb478a0e70fb7a72a5438dbe3b566bb372384c8ef4194727-image.png)

<br />

2. **Game Rules** This section allows Producers to configure instructional content and game rules shown to players.

   1. How to Play Screen: Enable this option to display a How to Play screen explaining the gameplay.
   2. Rules: Enable this option to display a Rules screen before the game begins.
   3. Rules Title: Defines the title displayed on the rules page.

      Example:

      Guess the Image Rules
   4. Rules Information: Allows Producers to provide instructions explaining how to play the game.
   5. Terms & Conditions: Optional field to add legal terms or participation conditions.
   6. URL: Allows Producers to link to an external Terms & Conditions page.

   ![](https://files.readme.io/8db5b3ecfa845c49cfcc38bba361f8745796feca7520f28f8b1612e1ef0f7975-image.png)

   <br />
3. **Game Copies** Configure game text elements:

   1. Welcome screen with a custom greeting and a start button
   2. End screen with closing message
   3. Result screen with two display types: Single/Score Based

   <br />

   ![](https://files.readme.io/211d9ccb2826c2c688368fa726daa02270b28468ec45f18516db57504685e8fc-image.png)
4. **Word Database**

   1. You can set up target words and images for each date, with support for word lengths ranging from 5 to 10 letters.
   2. By default, we provide a database of pre-configured words for 15 days.
   3. Currently, manual word and images entry is the supported method for adding words to the database. You can add or delete the rows and columns to manage the words.
   4. <br />

   ![](https://files.readme.io/0d4951a78e87a5d385afc0045512316824baf01183c92ede39d434437143633d-image.png)

   <br />
5. **Theme Setup**
   1. In this step, you can customize the visual branding and theme elements of your game.
   2. This is part of the game's customization process, allowing you to maintain brand consistency and create a unique visual identity for your GTI implementation. The theme setup ensures your game matches your brand's visual guidelines and style requirements.
   3. **Please note:**

      1. The structure of the game stays the same. Positioning, adding, and resizing of components cannot be done
      2. Only colors/background images and text copies can be customised
      3. Brand Logo -  Max size: 42x300 pixels
      4. Game Font: Applied to all text except letters input in the Grid.
      5. Grid Font: Applied to only Letters in the Grid.
      6. Game logo: Max size: 42x300 pixels
      7. Sponsor Logo: Max size: 42x300 pixels
      8. Background image: Recommended size 1080x1920 , max size 1mb

      <br />

      ![](https://files.readme.io/fe69cbb447236fde487b2d0e7cf2b549e70dbe32fb0504dd566cdf603e5efa53-image.png)
6. **Social features**The section includes toggles for showing user stats and enabling stat sharing capabilities.

   1. Players can customize a share message (defaulted to "Join me in today's word puzzle") to invite others. The Deeplink feature allows configuration of deep linking functionality, along with a countdown toggle that displays a countdown when today's game ends but the new game hasn't started yet, indicating when the next game day begins.
   2. Count Down features when enabled, displays a countdown when today's game ends but the new game hasn't started yet, indicating when the next game day begins.

   <br />

   ![](https://files.readme.io/b3de62c1f9586fd0a38f83d1c2de1515d6989c1cbf6620eaa1367151b3da3f09-image.png)
7. **Localization**

   1. Localized content
   2. New localized data

   <br />

   ![](https://files.readme.io/a94c92cb7dfb51e690b68ddda20adc8a5b221fa7933fba24320df20a8d417bb7-image.png)
8. **Live Game Manager**
   1. This section provides real-time management capabilities for your GTI game.
   2. This interface includes a "Publish Game" button for launching your game and displays the word and image timeline.

<Image align="right" src="https://files.readme.io/04d15f747ea21378258db81cc6860434a087bebbe21fef93c6cc51def06e9ade-image.png" />

<br />
