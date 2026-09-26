# Tiniest Cloud

Build a web app in a conversation with Claude, or with your coding agent, and put it online at
[Tiniest Cloud](https://tiniest.cloud). Every app gets sign-in, per-user storage, realtime, push
notifications, scheduled jobs and an AI model — with no keys to manage and no backend to write.

This plugin adds two things:

- **The Tiniest Cloud MCP server** (`https://app.tiniest.cloud/mcp`). Claude can deploy a
  folder and get a live URL, share an app by email, roll back to an earlier version, connect a
  third-party API without putting its key in the page, schedule recurring work, and put an app
  on your own domain, and read or change the data an app has saved.
- **The `tiny` skill**, which tells Claude how to build for the platform — a plain static
  site using the `tiny` SDK, no login flow, no `localStorage`, no backend — and to fetch the
  current SDK reference with the `tiny_guide` tool before it starts.

## Install

**Claude (web, desktop, mobile and Cowork):** open Customize → Plugins → Discover, find
*Tiniest Cloud* and add it, then connect it on the plugin's Connectors tab.

**Cursor:** find *Tiniest Cloud* in the Marketplace and click Add.

**Claude Code:**

    /plugin marketplace add mohamedyameen/tiniest-cloud-plugin
    /plugin install tiniest-cloud@tiniest-cloud

**Gemini CLI:**

    gemini extensions install https://github.com/mohamedyameen/tiniest-cloud-plugin

Then run `/mcp auth tiniest-cloud` inside Gemini CLI to sign in.

**Any other MCP client:** add the server `https://app.tiniest.cloud/mcp` (Streamable HTTP).

The first time Claude uses a Tiniest Cloud tool, your browser opens to sign in (or create a
free account). There is no API key to paste.

## Try it

- "Build a small expense tracker and put it on Tiniest Cloud."
- "What apps do I have on Tiniest Cloud?"
- "Share my notes app with sam@example.com."

## What it sends

Everything goes to Tiniest Cloud at `app.tiniest.cloud`, and only when Claude calls one of its
tools on your behalf:

- the files of an app you ask Claude to deploy;
- the email addresses of people you share an app with or add to a space;
- entries you ask Claude to write to an app's saved data, and the details of any API connection
  or scheduled job you set up.

Reading tools send only the name of the app and what to look up. The plugin itself stores
nothing and runs no code on your machine; the skill is text, and the server is hosted.

## Privacy and support

- Privacy policy: https://tiniest.cloud/privacy
- Terms: https://tiniest.cloud/terms
- Support: support@tiniest.cloud

This repository contains only the plugin: its manifests, the MCP server address and the skill.
The server itself is hosted by Tiniest Cloud.
