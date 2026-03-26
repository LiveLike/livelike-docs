---
title: Pick Your Team CMS Guide
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
Pick Your Team is a strategic game where users select players to create their ideal sports team. The game features include Strategic team building with players making thoughtful choices about team composition, and Customizable theming to match your brand identity

<br />

***

Pick Your Team is available in the experiences list once you login and choose your application.

![](https://files.readme.io/12ae6be9b4d151532210d7f23834fd448821439c778e728183cbc1b4600bfa3c-image.png)

To begin, either select an existing game or click "Create New" to start fresh. The setup process consists of 6 key steps.

<Image align="center" src="https://files.readme.io/853e66744919aee6d9f12b2f68ab2712118c55cf5678bc080a1d1d25dd1811a0-welcome_screen.gif" />

1. **Welcome Screen**  
   This is the initial configuration page where you set up the player's first interaction with the Pick Your Team game. Here you can customize the initial setup and welcome experience for your players when they first enter the game.
   1. **Welcome Screen Configuration:**
      1. **Button Label**
         1. Customize the start button text
         2. Default value: "Start"
         3. This is the button players will click to begin team selection
   2. **Welcome Text**
      1. Set the main welcome message
      2. Example: "Welcome to Pick Your Team!"
      3. Keep it brief and engaging
   3. **Text Information**
      1. Add detailed instructions for players
      2. Include step-by-step guidance
   4. **Terms & Conditions**
      1. Add your terms and conditions text
      2. Example URL format: [www.samplewebsite/terms.html](http://www.samplewebsite/terms.html)
   5. **Rules Section**
      1. Toggle to enable/disable rules display
      2. Set a custom rules title (e.g., "Team Selection Rules")
      3. Add specific game rules in the Rules Information field
      4. Common rules examples:
         1. Each player can only be selected once
         2. No changes allowed after team confirmation

![](https://files.readme.io/6e1bd8b08870a389f6b07ff2c49e8dfdbf9264ec04386deede8ea6d13a692087-image.png)

2. **Sports and Tournaments:**  
   This section allows you to set up the core elements of your Pick Your Team game by configuring the sport, data source, and tournament settings.

   1. **Sport Selection**: Choose the sport for your game (e.g., Football). This determines the available tournaments and team options.
   2. **Data Source Configuration**: Two options for adding player and team data:
      1. Source Integration
      2. CSV File Upload (coming soon)
   3. **Tournament Setup**
      1. Select a specific tournament (e.g., UEFA Champions League)
      2. Choose participating teams from the tournament
      3. Select relevant fixtures/matches
   4. **Select game type**
      1. Same team: Users can only pick players from one team
      2. All teams: Users can pick players from any participating team
   5. **Key Considerations:**
      1. Ensure data source credentials are valid
      2. Verify that all selected teams have complete player data
      3. Check fixture dates align with your game schedule

![](https://files.readme.io/91b7c6a0bb86a0737c58a9912844b3256fe3c31828fc688db2a18fac56557b94-image.png)

<br />

3. **Media Library**  
   The Media Library section allows you to manage and upload images for teams and players in your Pick Your Team game.
   1. **Image Upload Process**
      1. **Download Template**
         1. Click the "Download images template" link to get the CSV format
         2. Use this template to prepare your image information
      2. **CSV File Upload**
         1. Click "Browse file" to upload your images CSV file
         2. The file must follow the template format
         3. Contains image information for both teams and players
   2. **Image Requirements**
      1. Recommended minimum size: 400 x 900 pixels
      2. Maximum file size: 1 MB per image
      3. Supported format: JPG/JPEG
   3. **Preview Section**
      1. Select teams from the dropdown to preview their assets
      2. View both team and player images
   4. **Key Features**
      1. Skip this step, toggle available if needed
      2. Preview functionality to verify uploaded images
      3. Hierarchical display with team and player images
      4. Organized view of all media assets
   5. **Best Practices**
      1. Ensure all images meet the size requirements
      2. Verify all required images are included in the CSV
      3. Check image quality in the preview before proceeding
      4. Maintain consistent image dimensions for a professional appearance

**Note: The media library is crucial for creating an engaging visual experience. Proper image assets help players easily identify teams and players during the selection process.**

![](https://files.readme.io/be2e6b69570a1d5726a2aa4b6e7633620f69eee85d221f797caec8fb020f4468-image.png)

4. **Rewards and Social Features**
   1. The Rewards and Social step allows you to configure how players share their game experience, earn points, and compete on leaderboards. This step is divided into two areas: **Social Sharing and Points & Rewards**.
   2. **Key Features:**
      1. Allow share image toggle
      2. Customizable share message
      3. Deeplink configuration
      4. Image download options
   3. **Process Overview:**
      1. Enable or disable image sharing functionality
      2. Customize the default share message (e.g., "Join me in today's pick your team")
      3. Configure the deeplink URL for game access
      4. Control whether users can download images
      5. The social features help increase engagement and virality by letting players share their team selections and invite others to participate.

![](https://files.readme.io/d82a9f0d1c3f6ea66fd64f2db4a4c65ebd3c2a93f1cf8f4e0c379ca04f6c8985-image.png)

5. **Theming**
   1. The Theme & Branding section allows you to customize the visual identity of your Pick Your Team game. The interface is divided into different tabs: Brand & Theme name, Welcome screen, Team/fixtures, The playground, Players list, and Information.
   2. **Theme Configuration:**
      1. Choose between using an existing theme or creating a new one
      2. Select theme from dropdown (e.g., "Default (LiveLike)")
      3. Option to customize various game screens
   3. **Brand Assets:**
      1. Brand Logo
         1. Recommended size: 60px × 60px
         2. Formats: PNG, JPG
         3. Maximum file size: 1 MB
      2. **Sponsor Logo**
         1. Recommended size: 60px × 60px
         2. Formats: PNG, JPG
         3. Maximum file size: 1 MB
      3. **Game Logo**
         1. Two options:
            1. Text Label: Use text for game title
            2. Game Logo: Upload custom logo
         2. **Recommended: 16:5 aspect ratio**
         3. Formats: PNG, JPG
         4. Maximum file size: 1 MB
   4. **Important Notes:**
      1. **Structure Limitations:**
         1. Basic game flow cannot be modified
         2. Component positioning is fixed
         3. Core mechanics remain consistent
      2. **Customization Scope:**
         1. Colors and backgrounds are customizable
         2. Text content can be modified on welcome and results screens
         3. Player data structure must follow predefined format
      3. **Performance Considerations:**
         1. Optimize image sizes for better loading

**Each section includes a "Browse file" button for easy upload and information icons (?) for additional guidance.**

<Image align="center" src="https://files.readme.io/dc4ec287f26d3e1040b36a1e65adca1385ed4b182294b3e127e285b03eb0baba-Screenshot_2025-01-17_at_16.44.17.png" />

6. **Localization**

   The Localization step allows producers to configure language settings, upload language-specific fonts, and manage translated game content. This step has two tabs: Configuration and Game Content.

   <br />

   ![](https://files.readme.io/40b4e18757330c035dc0b3d2df6303ce714675cd89cae6fcd8b9e8ba25d9eb62-image.png)

   <br />
7. **Schedule**
   1. **Control game availability:**
      1. Publish immediately
      2. Schedule for future date/time

![](https://files.readme.io/a512427165a1ea73a594254dfb7322b1883fc3f4dfdf82453de92d323f5a7f75-image.png)

7. **Preview**  
   Click on the 3 dot icon and click Preview to preview the experience you created.

<Image align="center" src="https://files.readme.io/71dc46116d8965912b1fe593e503cc85b3e2b618c31ab7e796648f389d571cc8-Screenshot_2025-01-17_at_16.50.17.png" />

<br />
