---
title: MCP Server
excerpt: >-
  LiveLike MCP server enabling AI Assistant tool based MCP Client to manage
  LiveLike resources.
deprecated: false
hidden: false
metadata:
  description: >-
    LiveLike MCP server enabling AI Assistant tool based MCP Client to manage
    LiveLike resources.
  robots: index
---
A Model Context Protocol (MCP) server for interacting with LiveLike's engagement platform. This server enables AI assistants to manage LiveLike programs and interactive widgets through a standardized interface. <Anchor label="LiveLike MCP" target="_blank" href="https://www.npmjs.com/package/@livelike/mcp">LiveLike MCP</Anchor> is available as part of NPM package

## Key Features

* **Program Management**: Create, read, update, and delete LiveLike programs
* **Interactive Widgets**: Manage text quiz, image quiz, text poll, image poll, text prediction, image prediction, emoji slider, text ask, alert, image number prediction, image number prediction follow-up, text prediction follow-up, image prediction follow-up widgets
* **Scheduling**: Schedule widgets to be published at specific times
* **Engagement Tracking**: Monitor user interactions and engagement metrics
* **Standardized Interface**: MCP-compliant API for easy integration with AI assistants

## Pre-requisite

* Node.js 20.x or newer
* VS Code, Cursor, Windsurf, Claude Desktop, or any other MCP client
* LiveLike API credentials (client ID and access token)

## Installation

### Install Node

* We recommend installing node using [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script)
* Once `nvm` is installed, use nvm to install latest Node 20.x.x version, set the installed version as current node version and set it as default node version by running below command.

```sh
nvm install 20 && nvm use 20 && nvm alias default 20
```

### MCP Client Config

**For Windows platform, refer[server config issues](#common-issues) for `command` where `PATH` env var is not needed to be set as part of MCP server config**

#### Cursor

1. Open Cursor Settings → MCP
2. Click Add new global MCP server
3. Add an entry for the LiveLike MCP, following the pattern below:

```json Unix
{
  "mcpServers": {
    "livelike": {
      "command": "npx",
      "args": ["-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```
```json Windows
{
  "mcpServers": {
    "livelike": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```

#### Claude Desktop

1. Open Settings → Developer
2. Click Edit Config
3. Open claude\_desktop\_config.json
4. Add the following configuration:

```json Unix
{
  "mcpServers": {
    "livelike": {
      "command": "npx",
      "args": ["-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```
```json Windows
{
  "mcpServers": {
    "livelike": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```

#### Windsurf

1. from the Windsurf Settings > Cascade > Plugins section.

```json Unix
{
  "mcpServers": {
    "livelike": {
      "command": "npx",
      "args": ["-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```
```json Windows
{
  "mcpServers": {
    "livelike": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```

#### VSCode

1. Open User Settings (JSON)
2. Add an MCP entry:

```json Unix
{
  "mcpServers": {
    "livelike": {
      "command": "npx",
      "args": ["-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```
```json Windows
{
  "mcpServers": {
    "livelike": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "@livelike/mcp"],
      "env": {
        "LIVELIKE_CLIENT_ID": "your_client_id",
        "LIVELIKE_ACCESS_TOKEN": "your_access_token",
      }
    }
  }
}
```

## Configuration

### Environment Variables

Set these environment variables before starting the server:

**LIVELIKE\_CLIENT\_ID=your\_client\_id**\
Your LiveLike Client ID

**LIVELIKE\_ACCESS\_TOKEN=your\_access\_token**\
[Your LiveLike Admin Access Token](https://docs.livelike.com/reference/authentication#admin-access-token)

## Available Tools

### Program Management

* `list_programs`: Retrieve a list of programs with filtering and pagination
* `get_program`: Get details of a specific program
* `create_program`: Create a new program
* `update_program`: Modify an existing program
* `delete_program`: Remove a program
* `program_action`: Mark a program as started or stopped

### Widget Management

* `list_widgets`: Retrieve a list of widgets with filtering and pagination
* `get_widget`: Get details of a specific widget
* `delete_widget`: Remove a widget
* `schedule_widget`: Schedule a widget to be published at a specific time

### Text Quiz Widgets

* `create_text_quiz_widget`: Create a new text quiz widget
* `update_text_quiz_widget`: Modify an existing text quiz widget

### Text Poll Widgets

* `create_text_poll_widget`: Create a new text poll widget
* `update_text_poll_widget`: Modify an existing text poll widget

### Image Quiz Widgets

* `create_image_quiz_widget`: Create a new image quiz widget
* `update_image_quiz_widget`: Modify an existing image quiz widget

### Image Poll Widgets

* `create_image_poll_widget`: Create a new image poll widget
* `update_image_poll_widget`: Modify an existing image poll widget

### Text Prediction Widgets

* `create_text_prediction_widget`: Create a new text prediction widget
* `update_text_prediction_widget`: Modify an existing text prediction widget
* `publish_text_prediction_followup_widget`: Publish text prediction followup widget after updating with correct prediction

### Image Number Prediction Widgets

* `create_image_number_prediction_widget`: Create a new image number prediction widget
* `update_image_number_prediction_widget`: Modify an existing image number prediction widget
* `publish_number_prediction_followup_widget`: Publish number prediction followup widget after updating with correct prediction

## Troubleshooting

### Common Issues

1. for server related issue like npx command not found or node not found

   Identify `npx` and `Node` binaries path

   Get the `npx` path and installed node version `bin` path
   ```sh
   which npx
   ```
   eg: `/Users/<user-account-name>/.nvm/versions/node/v20.19.2/bin/npx`
   * use `/Users/<user-account-name>/.nvm/versions/node/v20.19.2/bin/npx` as mcp server command (referred as `<npx_path>` in below mcp client config)
   * add node bin path `/Users/<user-account-name>/.nvm/versions/node/v20.19.2/bin` to `PATH` env var (referred as `<node_bin_path>` in below mcp client config)
   * ```json MCP server config
     "livelike": {
        "command": "<npx_path>/npx",
        "args": ["-y", "@livelike/mcp"],
        "env": {
           "LIVELIKE_CLIENT_ID": "your_client_id",
           "LIVELIKE_ACCESS_TOKEN": "your_access_token",
           "PATH": "<node_bin_path>:/usr/local/bin:/usr/bin:/bin"
        }
     }

     ```
2. **Server Config Issues**

   * For windows platform, use below config, refer [related blog](https://apidog.com/blog/how-to-fix-cursor-ai-mcp-feature-client-closed-error/) for mode details.

   ```json
   {
     "command": "cmd.exe",
     "args": ["/c", "npx", "-y", "@livelike/mcp"],
     "env": {
       "LIVELIKE_CLIENT_ID": "your_client_id",
       "LIVELIKE_ACCESS_TOKEN": "your_access_token"
     }
   }
   ```
3. **Authentication Errors**

   * Verify `LIVELIKE_CLIENT_ID` and `LIVELIKE_ACCESS_TOKEN` are correct
   * Ensure the credentials have the necessary permissions
4. **Connection Issues**

   * Check if the LiveLike API is accessible from your network