# Tiniest Cloud

Deploy web apps to [Tiniest Cloud](https://tiniest.cloud) from your coding agent. Every app gets
sign-in, per-user storage, realtime, push notifications, scheduled jobs and an AI model — with no
keys to manage and no backend to write.

This plugin adds two things:

- **The Tiniest Cloud MCP server** (`https://app.tiniest.cloud/mcp`). Your agent can deploy a
  folder and get a live URL, share an app by email, roll back to an earlier version, connect a
  third-party API without putting its key in the page, schedule recurring work, and put an app
  on your own domain.
- **The `tiny` skill**, which tells the agent how to build for the platform — a plain static
  site using the `tiny` SDK, no login flow, no `localStorage`, no backend — and to fetch the
  current SDK reference with the `tiny_guide` tool before it starts.

## Install

**Cursor:** find *Tiniest Cloud* in the Marketplace and click Add.

**Claude Code:**

    /plugin marketplace add mohamedyameen/tiniest-cloud-plugin
    /plugin install tiniest-cloud@tiniest-cloud

**Gemini CLI:**

    gemini extensions install https://github.com/mohamedyameen/tiniest-cloud-plugin

Then run `/mcp auth tiniest-cloud` inside Gemini CLI to sign in.

**Cline, or any other MCP client:** add the server `https://app.tiniest.cloud/mcp`
(Streamable HTTP). Step-by-step setup, including a token fallback, is in
[llms-install.md](llms-install.md).

The first time the agent uses a Tiniest Cloud tool, your browser opens to sign in (or create a
free account). There is no API key to paste.

## Try it

- "Build a small expense tracker and put it on Tiniest Cloud."
- "What apps do I have on Tiniest Cloud?"
- "Share my notes app with sam@example.com."

## Privacy and support

- Privacy policy: https://tiniest.cloud/privacy
- Terms: https://tiniest.cloud/terms
- Support: support@tiniest.cloud

This repository contains only the plugin: its manifests, the MCP server address and the skill.
The server itself is hosted by Tiniest Cloud.
