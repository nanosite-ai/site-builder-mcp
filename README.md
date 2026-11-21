# NanoSite MCP: build websites and online stores from your AI app

Connect [NanoSite](https://nanosite.ai) to the AI app you already use (GitHub Copilot, Claude, ChatGPT, Cursor,
Gemini CLI or any other app that supports **MCP**). From that chat you can start, edit and publish a website or
online store, and run the store's products, orders and discounts. Your agent gets the same tools as NanoSite's
own AI builder. You don't install anything, and you don't need to be a developer.

This is a **hosted, remote MCP server**. This repository holds only its documentation: the server runs on
nanosite.ai. Full guide: **[nanosite.ai/docs/connect-ai-agent](https://nanosite.ai/docs/connect-ai-agent)**.

| | |
|---|---|
| **URL** | `https://nanosite.ai/api/mcp` |
| **Transport** | Streamable HTTP |
| **Sign-in** | OAuth: your app opens a NanoSite page where you log in and click **Allow** |
| **Registry name** | `ai.nanosite/nanosite` |

## What it does

- **Start a project**: pick a template and create a new website or store on your NanoSite account.
- **Edit pages**: read, search and change the project's files (pages, sections, text, styles), several files
  at once if needed. Every change is saved as its own version, which you can undo from the NanoSite builder.
- **Run your store**: add and edit products, collections, prices and stock; look at orders; create discount
  codes; manage shipping, tax and settings; set up store add-ons.
- **Images**: create or edit images for your pages, resize them, polish product photos (white background,
  lighting, color, upscale), and host an image from a link.
- **Preview and publish**: get a private draft link after each change, check that the build passes, and publish
  when you say so.

## Set it up

You need a NanoSite account. You don't need a project yet: the agent can create one.

### VS Code (GitHub Copilot)

Add this to `.vscode/mcp.json`, or run **MCP: Add Server** from the command palette:

```json
{
  "servers": {
    "nanosite": { "type": "http", "url": "https://nanosite.ai/api/mcp" }
  }
}
```

Start the server from the file or the **MCP Servers** view, sign in when asked, and use Copilot Chat in
**Agent** mode.

### Claude Code

```bash
claude mcp add --transport http nanosite https://nanosite.ai/api/mcp
```

Then run `/mcp`, pick **nanosite** and choose **Authenticate**.

### Claude (claude.ai and Claude Desktop)

**Settings → Connectors → Add custom connector**. Name it `NanoSite`, use the URL `https://nanosite.ai/api/mcp`,
then click **Connect** and **Allow**.

### Cursor

In `~/.cursor/mcp.json` or `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "nanosite": { "url": "https://nanosite.ai/api/mcp" }
  }
}
```

Then click **Login** next to nanosite in **Cursor Settings → MCP**.

### Gemini CLI

In `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "nanosite": { "httpUrl": "https://nanosite.ai/api/mcp" }
  }
}
```

Then run `/mcp auth nanosite`.

### Any other MCP app

Add a remote MCP server with the URL `https://nanosite.ai/api/mcp` (Streamable HTTP). If the app can't sign in
with OAuth, create an access token on NanoSite under **Account settings → Connected apps and devices** and send
it as `Authorization: Bearer <token>`.

## How to use it

Say which project you mean. The agent can list your projects if you're not sure. For example:

- *"Create a new store for my candles from a template you think fits, and call it Candle Co."*
- *"In my Candle Co store, add a product: Lavender soy candle, $24, 30 in stock."*
- *"Which orders from this week haven't shipped yet?"*
- *"Add a 10% off code SPRING for the next two weeks."*
- *"Make the homepage hero full width and change the headline to 'Hand-poured in Lisbon'."*
- *"Put the photos of my three newest products on a white background and show me the options."*
- *"Show me the draft, then publish it."*

Nothing goes live until you publish. Store data (products, prices, discount codes) changes right away, the same
as editing it in NanoSite.

## Tools

| Area | Tools |
|---|---|
| Projects | `listProjects`, `listTemplates`, `createProject` |
| Files | `listFiles`, `grepFiles`, `readFile`, `writeFile`, `writeFiles`, `replaceInFile`, `deleteFile`, `getProjectDependencies` |
| Guides | `loadSkill`, `loadRule` |
| Store data | `listEcommerceAdminApi`, `ecommerceAdminRead`, `ecommerceAdmin` |
| Add-ons | `listAddOns`, `configureAddOn`, `setAddOnEnabled`, `testAddOn` |
| Images | `listImages`, `generateImage`, `resizeImage`, `enhanceProductImage`, `importImage` |
| Preview and publish | `getPreviewLink`, `checkBuild`, `publish`, `getPublishStatus` |

Every tool that changes or deletes something is marked as such, so apps that ask before acting will ask you
first. Publishing and turning an add-on on or off always need your clear yes.

## Your account and safety

- The agent reaches only the projects you're a member of, with the permissions you allowed.
- Payment keys and other secrets are never shown to the agent. You enter them on nanosite.ai.
- To disconnect, remove the connector in your app, or revoke it under **Account settings → Connected apps and
  devices** on NanoSite.

## Support

Questions or problems: email [info@nanosite.ai](mailto:info@nanosite.ai) and say which AI app you use, or
[open an issue](https://github.com/nanosite-ai/site-builder-mcp/issues). Privacy:
[nanosite.ai/privacy-policy](https://nanosite.ai/privacy-policy#connected-ai-apps).
