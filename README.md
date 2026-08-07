# 📜 Components V2 Builder

A visual, browser-based editor for building Discord **Components V2** webhook messages — no manual JSON required.
Assemble containers, text blocks, sections, media galleries, and action rows on a canvas, watch a live Discord-style preview update as you go, and send the result straight to a webhook when you're ready. Everything runs entirely in the browser: there's no server, no build step, and no dependency to install.

## Why this exists

Discord's Components V2 message format is powerful but verbose — building anything beyond a simple embed by hand means writing and re-writing nested JSON, restarting whenever a bracket is out of place. This tool replaces that loop with a drag-and-drop builder and an instant preview, so you can focus on the message you're designing instead of the payload structure behind it.

## Features

- **Component palette** — add Containers, Text Displays, Sections, Media Galleries, Separators, and Action Rows to your message
- **Nested containers** — containers hold their own children, so layouts can be composed and organized visually
- **Drag-and-drop reordering** — rearrange components directly in the builder panel
- **Live Discord-style preview** — see exactly how the message will render before you send it
- **JSON payload inspector** — view and copy the generated Components V2 JSON at any time, for use elsewhere or for debugging
- **Rich section support** — attach a thumbnail or a link button as an accessory to any section
- **Container styling** — optional accent color and spoiler toggle per container
- **One-click send** — paste a webhook URL and post the message directly from the browser
- **Identity overrides** — set a custom username and avatar for the webhook post, per message
- **Zero setup** — a single static HTML file; open it and start building

## Getting started

### Option 1 — Use it online

Open the hosted version: **[Live demo](#)** *(replace with your GitHub Pages URL once deployed)*

### Option 2 — Run it locally

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

Then open `index.html` in any modern browser. That's the entire setup.

## Usage

1. **Add a webhook URL.** Paste your Discord webhook URL into the field at the top of the builder. Optionally set a username or avatar override for this message.
2. **Build your message.** Use the component buttons to add Containers, Text Displays, Sections, Media Galleries, Separators, and Action Rows. Nest components inside containers and drag to reorder.
3. **Preview as you go.** The right-hand panel renders a live, Discord-accurate preview of your message.
4. **Inspect the JSON (optional).** Switch to the JSON payload tab to view or copy the raw structure Discord will receive.
5. **Send it.** Click **Send to Discord** to post the message via your webhook.

## How it works

The builder maintains an in-memory component tree that mirrors Discord's Components V2 schema. Each addition, edit, or reorder updates that tree, which is then rendered three ways in parallel: the editable builder panel, the live preview, and the JSON payload. On send, the tree is serialized into a valid Components V2 payload (flagged with the `IS_COMPONENTS_V2` message flag) and POSTed to the webhook URL you provide.

No part of this process touches a server you don't control — the only network request the page makes is the direct call to Discord's API when you click **Send**.

## Security

Your webhook URL functions like a password: anyone who has it can post messages to that channel. This tool:

- Never stores your webhook URL, message content, or any other input outside your browser tab
- Never transmits data to any third party or analytics service
- Sends messages directly from your browser to Discord's API — nothing passes through an intermediary server

Don't share screenshots, recordings, or copies of this page with your webhook URL already filled in.

## Browser support

Works in any modern evergreen browser (Chrome, Firefox, Edge, Safari). No Internet Explorer support.

## Contributing

Issues and pull requests are welcome. If you're proposing a new component type or feature, please open an issue first to discuss it — Discord's Components V2 schema has some sharp edges worth aligning on before implementation.
