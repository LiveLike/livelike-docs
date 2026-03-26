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

   The Rewards and Social step allows you to configure how players share their game experience, earn points, and compete on leaderboards. This step is divided into two areas: **Social Sharing and Points & Rewards**.

   <br />

   ### Social Sharing

   This section focuses on customizing sharing options and social engagement settings.

   1. **Allow Share Image** _(toggle)_
      1. Enable to allow players to share a generated image of their team on social media

   2. **Share Message**
      1. Customize the default text that accompanies a shared post
      2. Example: `Just picked my dream team! Ready to compete! 🏆 #PickYourTeam`

   3. **Deeplink**
      1. Enter the URL that the share link will direct recipients to when clicked
      2. Example: `https://www.livelike.com`

   4. **Preview — Include Image URL?** _(checkbox)_
      1. When **enabled** — a preview-enabled share link is generated and the deeplink is embedded within the preview page
      2. When **disabled** — the deeplink is included directly in the share message
      3. Note: Some platforms do not display link previews when multiple links are shared — this setting ensures consistent behavior across platforms

   5. **Subdomain**
      1. Enter your organization's subdomain to generate a branded share link
      2. Example: `myorg`
      3. The generated share link will follow the format: `https://link.livelike.games/<share_code>`

   6. **Allow Download Image** _(toggle)_
      1. Enable to allow players to download their team image directly to their device

   ### Points & Rewards

   1. **Enable Points Per Correct Answer** _(toggle)_
      1. Enable to award points to players based on their team performance after resolution

   2. **Points Per Correct Answer**
      1. Enter the number of points awarded for each correct player pick
      2. Default value: `10`

   3. **Reward Points for Correct Formation** _(checkbox)_
      1. Check this box to award additional points when a player's chosen formation matches the actual match formation
      2. Requires **Enable Formation Option** to be turned on in Step 2

   4. **Points Label**
      1. Enter the label used to display points to players within the game
      2. Default value: `Points`

   5. **Select Reward Item**
      1. Choose a reward item from the dropdown to grant to players upon earning points

   ### Leaderboard

   1. **Select Existing Leaderboard**
      1. Attach an existing leaderboard to this game
      2. > **Note:** Any leaderboard attached here will be treated as a **global leaderboard** and shared across all applicable fixtures

   2. **Select Leaderboard Type**
      1. Choose the leaderboard aggregation type to determine how scores are grouped and ranked
      2. Example: `Monthly, Fixture`

   ### Key Features

   1. Social features increase engagement and virality by letting players share their team selections and invite others to participate
   2. Points and rewards incentivize accurate team selections
   3. Leaderboard integration creates competitive engagement across fixtures

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

   ### Tab: Configuration

   1. **Language**
      1. **Add Language** — Select a language using the language code dropdown and click **Add Language** to support it in your game
         * Example: `en` for English
      2. **Select Default Language** — Choose the default language displayed to players when they first enter the game
         * Example: `(en) English`
      3. **Allow Language Switch** _(toggle)_ — Enable to allow players to switch between supported languages within the game interface

   2. **Font**
      1. **Select Language** — Choose the language for which you want to assign a custom font
      2. **Language Font** — Upload a custom font file (.ttf) to apply for the selected language
         * Click **Browse File** to upload your font

   ### Tab: Game Content

   1. Use this tab to manage translated text strings for each language added in the Configuration tab
   2. Enter localized versions of all in-game labels, messages, and UI text
   3. Each added language will have its own column of translatable strings

   ***

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

## Managing Your Games

### Game Instances

Once your Pick Your Team game is created, it will appear in the **Game Instances** list. This page provides a full overview of all games created within your application.

**Page Tabs**

| Tab                | Description                                                                  |
| ------------------ | ---------------------------------------------------------------------------- |
| **Game Instances** | Lists all created Pick Your Team games with their current status and details |
| **Activity Logs**  | View a history of all actions taken on games within this application         |
| **What's New**     | See the latest updates and new features added to Pick Your Team              |

**Game List Columns**

| Column         | Description                                                                             |
| -------------- | --------------------------------------------------------------------------------------- |
| **Name**       | The name of the game instance                                                           |
| **Created By** | The producer who created the game                                                       |
| **Created On** | The date the game was created                                                           |
| **Updated By** | The producer who last made changes                                                      |
| **Updated On** | When the game was last updated                                                          |
| **Type**       | Current status — **Active** (live and visible to players) or **Inactive** (unpublished) |

### Three-Dot Menu Options

Click the **⋮** icon on any game instance to access the following actions:

| Option             | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| **Preview**        | Preview the game experience as a player without publishing            |
| **Unpublish Game** | Take the game offline — it will no longer be visible to players       |
| **Edit**           | Return to the 7-step setup flow to modify the game configuration      |
| **Control Panel**  | Open the Control Panel to manage fixture resolution                   |
| **Delete**         | Permanently delete the game instance _(this action cannot be undone)_ |
| **Documentation**  | Open the Pick Your Team documentation directly from the CMS           |

***

## Control Panel

The Control Panel is where producers manage the **resolution** of each fixture — publishing the official starting XI and formation that will be used to score player submissions.

To access the Control Panel, click the **⋮** menu on any game instance and select **Control Panel**.

![](https://files.readme.io/a730949b9e5f0bb6046a757f17b66744d3b8a40f376168a4c1c201370ea53411-image.png)

![](https://files.readme.io/39c607c9806e5b16514de49117ad0148cbc12a6fd3831d9013972018d40c35c7-image.png)

![](https://files.readme.io/7197821eac10e203e0a8b24bf1894d85a9e5ff565fc01316c296e5da09d700d0-image.png)

<br />

### AI Resolution vs. Manual Resolution

> **If Enable AI Resolution is turned on**, the system will **automatically resolve the lineup 30 minutes after the match start time** using AI and live data feed. In this case, you do **not** need to manually select the team or players — resolution happens automatically.
>
> **If AI resolution fails** for a fixture, go to the fixture in the Control Panel and click **Publish with AI**. This will publish the lineup without requiring manual player selection.
>
> **Manual resolution** (steps below) is only required when AI resolution is disabled or unavailable.

### Section 1: Select Fixture

1. **Enable AI Resolution** _(toggle)_
   1. Enable to allow the system to automatically resolve lineups using AI and live data feed
   2. Automatic resolution will occur **30 minutes after the match start time**

2. **Search**
   1. Search for a specific fixture by fixture ID, team ID, or team name

3. **Fixture Filter Tabs**
   1. **Past** — Fixtures that have already taken place
   2. **Future** — Upcoming fixtures that have not yet been played
   3. **Published** — Fixtures that are live and visible to players
   4. **Not Published** — Fixtures not yet visible to players

4. Each fixture card displays the tournament name, match teams, and kickoff date and time (UTC)

5. Fixtures with a green checkmark have already been resolved

6. Select a fixture to proceed to **Select Team**

### Section 2: Select Team

1. After selecting a fixture, choose which team's starting XI you want to manage

2. The **Fixture ID** is displayed for reference and can be copied using the copy icon

3. Teams are shown with their availability status:
   * **Available** — This team can be selected for resolution
   * **Not Available** — This team cannot be managed for this fixture

4. Select the available team to proceed to **Select Players**

5. **Publish with AI** _(button)_
   1. Click to publish the resolved lineup using AI and data feed, without manually selecting players
   2. Use this as a **fallback if automatic AI resolution has failed** for a fixture
   3. Available once a fixture and team have been selected

### Section 3: Select Players

This section is only required for **manual resolution**.

1. **Fixture & Team Info**
   1. Displays the selected fixture and the team being managed
   2. Example: `Arsenal vs Chelsea — Mar 1, 2026 4:30 PM UTC | Team: Chelsea`

2. **Select Formation**
   1. Choose the formation used by the team in this match from the dropdown
   2. Used for formation-based scoring if the formation reward option is enabled

3. **Search Players**
   1. Search for a specific player by name within the squad

4. **Position Filters**
   1. Filter the player list by position to find players quickly:
      * **All** — Show all positions
      * **Goalkeeper** — Show goalkeepers only
      * **Defender** — Show defenders only
      * **Midfielder** — Show midfielders only
      * **Attacker** — Show attackers only

5. **Player List**
   1. Browse the full squad and click the **+** button next to each player to add them to the starting XI
   2. The counter at the top right tracks progress (e.g., `0/11 selected`)
   3. Select all 11 players and confirm the lineup to complete resolution

### Key Considerations

1. Always verify fixture selection before proceeding — resolution cannot easily be undone
2. If AI resolution is enabled, monitor the first few fixtures to confirm it is resolving correctly
3. Use **Publish with AI** as your first fallback option before resorting to manual selection
4. Ensure the correct formation is selected if formation-based scoring is enabled in your game
