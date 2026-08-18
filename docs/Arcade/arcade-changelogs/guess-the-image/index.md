---
title: Guess The Image
excerpt: >-
  A daily picture puzzle. Players see a pixelated image and guess what it shows,
  one letter at a time. Each wrong guess is a chance spent, and the picture
  sharpens as they go.
deprecated: false
hidden: false
metadata:
  robots: index
---
Releases are listed newest first. Only versions that change something visible or configurable get their own page.

## Releases

| Version     | Date        | What changed                                                                                       | Needs you to do anything?                    |
| ----------- | ----------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| [1.11.0](#) | 17 Aug 2026 | Highlights screen added. The game now sizes itself to its container instead of the browser window. | Optional, plus a check if you use custom CSS |
| 1.10.0      | 30 Jul 2026 | Keys give clearer feedback when pressed                                                            | No                                           |
| 1.9.0       | 30 Jul 2026 | Theming and screen-flow improvements                                                               | No                                           |
| 1.8.1       | 7 Jul 2026  | Fixed: default language failed when the SDK was missing                                            | No                                           |
| 1.8.0       | 26 May 2026 | Language and country support across events, and a language switch in settings                      | Optional                                     |
| 1.7.1       | 26 May 2026 | Fixed: could not type while the settings popup was open                                            | No                                           |
| 1.7.0       | 18 May 2026 | Analytics events and session tracking                                                              | No                                           |
| 1.6.1       | 12 May 2026 | Fixed: keyboard unresponsive when how-to-play was turned off                                       | No                                           |
| 1.6.0       | 8 May 2026  | Shows the answer image after the final attempt. Number keys added to the keyboard.                 | No                                           |
| 1.5.2       | 5 May 2026  | Fixed: typing registered on the welcome and stats screens                                          | No                                           |
| 1.5.1       | 24 Apr 2026 | Settings icon stays visible even when the word list runs out                                       | No                                           |
| 1.5.0       | 13 Mar 2026 | Separate mobile and desktop backgrounds for each screen                                            | Optional                                     |
| 1.4.0       | 12 Mar 2026 | Optional language switch and keyboard layout choice                                                | Optional                                     |
| 1.3.0       | 18 Nov 2025 | Custom loading screen                                                                              | Optional                                     |
| 1.2.0       | 29 Oct 2025 | Translation support                                                                                | Optional                                     |
| 1.1.0       | 17 Oct 2025 | Analytics                                                                                          | No                                           |

<Callout icon="📘" theme="info">
  ### Detailed notes start at 1.11.0

  Earlier releases are summarised in the table above. If you need the detail on an older version, ask the Arcade team.
</Callout>

## Screens in this game

Useful when reading a release note, since notes refer to screens by name.

| Screen     | What it is                                                                           |
| ---------- | ------------------------------------------------------------------------------------ |
| Welcome    | First screen. Shows the game logo and the Play button.                               |
| Game       | The picture, the letter grid, and the keyboard.                                      |
| End        | Shown once the day's puzzle is finished. Has Stats, and from 1.11.0 also Highlights. |
| Highlights | Read-only look back at the finished puzzle. Added in 1.11.0.                         |
| Stats      | The player's record: games played, win rate, streaks.                                |
| Settings   | Language and keyboard layout, where enabled.                                         |
