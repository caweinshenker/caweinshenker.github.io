---
layout: post
title: "Introducing playwright-mcp-electron: AI Automation for Electron Apps"
date: 2024-12-30
---

**playwright-mcp-electron** is a fork of Microsoft's Playwright MCP that adds support for automating Electron desktop applications through the Model Context Protocol (MCP).

## The Problem

The Model Context Protocol has changed how AI assistants interact with tools. Microsoft's [@playwright/mcp](https://github.com/microsoft/playwright-mcp) brought browser automation to MCP, enabling AI to navigate websites, fill forms, and extract data using accessibility-first automation.

But what about desktop applications? Many modern apps are built with Electron—VS Code, Slack, Discord, Notion, and countless others. Until now, there was no way for MCP-compatible AI assistants to interact with these apps.

## The Solution

`playwright-mcp-electron` extends Playwright MCP with full Electron support. Using Playwright's experimental Electron API, it can:

- **Launch and control Electron apps** - Connect to packaged `.app` bundles or development builds
- **Navigate using accessibility snapshots** - Same LLM-friendly approach as browser automation
- **Access the main process** - Execute code in Electron's Node.js main process
- **Manage multiple windows** - Switch between BrowserWindows in multi-window apps
- **Send IPC messages** - Communicate between main and renderer processes

## Installation

```bash
npm install playwright-mcp-electron
```

Or use directly with npx:

```bash
npx playwright-mcp-electron --electron-executable=/path/to/app --caps=electron
```

### Claude Code Setup

```bash
claude mcp add playwright-electron -- npx playwright-mcp-electron \
  --electron-executable=/Applications/YourApp.app/Contents/MacOS/YourApp \
  --caps=electron
```

## Available Tools

All standard Playwright MCP browser tools work with Electron windows:

- `browser_snapshot` - Get accessibility tree of current window
- `browser_click` - Click elements by reference
- `browser_type` - Type text into inputs
- `browser_navigate` - Navigate to URLs

Plus Electron-specific tools:

- `electron_evaluate` - Execute JavaScript in the main process
- `electron_windows` - List all open BrowserWindows
- `electron_select_window` - Switch active window
- `electron_app_info` - Get app name, version, paths
- `electron_ipc_send` - Send IPC messages to renderer

## Example Usage

```
User: Click the settings button and enable dark mode

Claude: [uses browser_snapshot to see current UI]
        [uses browser_click on settings button]
        [uses browser_snapshot to see settings panel]
        [uses browser_click on dark mode toggle]

        Done! Dark mode is now enabled.
```

The AI navigates the app, verifies UI states, and interacts with elements—all through natural language.

## Why This Exists

I submitted this as a PR to Microsoft's Playwright MCP, but they declined to maintain Electron support as it's outside their core scope. So I'm publishing it independently.

The packages:

- **[playwright-mcp-electron](https://www.npmjs.com/package/playwright-mcp-electron)** - The MCP server
- **[playwright-electron-mcp](https://www.npmjs.com/package/playwright-electron-mcp)** - Forked Playwright with Electron MCP support

Both are Apache-2.0 licensed with Microsoft credited as a contributor.

---

*[GitHub](https://github.com/caweinshenker/playwright-mcp) · [npm](https://www.npmjs.com/package/playwright-mcp-electron)*
