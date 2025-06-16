---
title: Supported Video Players
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Supported Video Players | LiveLike Developer Hub
  description: >-
    If you have a custom player or video production workflow, your developers
    can add custom plugins for common video players. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: spoiler-free-sync
      title: Spoiler Prevention
---
The LiveLike SDKs come bundled with support for common video players. If you have a custom player or video production workflow, your developers can add custom plugins for those situations.

> 📘 Video player integration not required
>
> An integration with a video player is only necessary for features like [Spoiler Prevention](doc:spoiler-free-sync). For general usage of features like widgets and chat, integration with the video player is not required.

## Supported Players

Support for some players and stream formats are maintained by LiveLike, and are bundled with the SDKs.

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Player
      </th>

      <th>
        Stream Format
      </th>

      <th>
        Timing
      </th>

      <th>
        Platform
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        AVPlayer
      </td>

      <td>
        HLS
      </td>

      <td>
        Program Date Time
      </td>

      <td>
        iOS
      </td>
    </tr>

    <tr>
      <td>
        ExoPlayer
      </td>

      <td>
        HLS
      </td>

      <td>
        Program Date Time
      </td>

      <td>
        Android
      </td>
    </tr>

    <tr>
      <td>
        Hls.js
      </td>

      <td>
        HLS
      </td>

      <td>
        Program Date Time
      </td>

      <td>
        JavaScript
      </td>
    </tr>
  </tbody>
</Table>
