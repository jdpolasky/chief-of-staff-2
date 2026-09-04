# Wiring Obsidian to your AI

*Last updated September 2026.*

This is the connection guide. It gets your Obsidian vault talking to an AI agent, so the agent can read and write your notes directly instead of you copying and pasting. Once this is done, your Chief of Staff can actually live in your vault. Setting up the Chief of Staff system itself is a separate step, covered in [`SETUP-HUMANS.md`](SETUP-HUMANS.md).

The whole thing rests on one idea. Your vault runs a small server that speaks a common language called MCP, the Model Context Protocol. Any AI agent that speaks MCP can connect to that one server. Claude Code, Codex, Gemini, and the rest all connect the same way. Only the line you paste into each one is different.

A word on models, since this is meant to work with any of them. An open model like Llama or Qwen running on your own machine does not talk to your vault by itself. The agent program wrapped around the model does that part. So when you read that this works with open models, what it means is that the agent you run can be pointed at an open model as its brain, and the vault connection is the same either way.

## What you need

Three things, all but one of them free.

1. **Obsidian**, the notes app your vault lives in. Free, from [obsidian.md](https://obsidian.md). Install it and create a vault, which is just a folder where Obsidian keeps your notes. You do not need any notes in it yet.
2. **An AI agent that can read and write files on your computer.** Claude Code is the one this project is built around and the one these instructions treat as the default. Codex CLI, Gemini CLI, and several others work too, and they each get their own line below. A paid plan is the one real cost here; the free tiers usually cannot run these agents.
3. **A few minutes.** That is the whole install.

## Step one: the vault side

This part is the same no matter which AI you use. You do it once.

**Install the connector plugin.** In Obsidian, open Settings, then Community plugins, then Browse. Search for **MCP Connector** by Stefano Ferri and install it. Turn it on. This plugin runs a small MCP server inside Obsidian itself, on your own machine, with its own on-device search. Nothing leaves your computer. It is the maintained successor to an older plugin called MCP Tools, which was archived in May 2026, so if an older guide points you at MCP Tools, this is what replaced it.

**Find the address.** Once the plugin is on, it serves at `http://127.0.0.1:27200/mcp`. If that port is busy it takes the next free one up to 27205, and it shows you the live address in its settings. That address is local to your machine and reachable by nothing outside it.

**Make a token.** In the plugin's settings, open the Access control panel and create a token. Copy it somewhere safe for the next step. Treat it like a password and never paste it into a note. You can make a separate token for each agent you connect, up to ten.

That is the vault side finished. The server is running and you have a token.

**A more established alternative.** The MCP Connector is new. If you would rather start from an older, far more widely used plugin, Local REST API with MCP also runs an MCP server inside Obsidian. It exposes fewer tools and has no built-in semantic search, though it has years of use behind it. Turn it on, take the address and API key from its settings, and register those in step two the same way you would the MCP Connector. Its endpoint uses HTTPS with a self-signed certificate, so some clients have to be told to trust it; the plugin's own docs cover that.

**Optional plugins, once the connection works.** None of these are required to connect. Add them later if you want them.

- **Tasks** and **Templater**, both actively maintained, if you want structured checkboxes and note templates.
- **Dataview**, for database-style queries inside notes. Obsidian now ships a built-in feature called Bases that covers simple tables and card views with no plugin at all, so reach for Dataview only when you need its more complex text queries. Dataview still works but has not seen an update since 2025.
- You do **not** need Smart Connections. The connector plugin already does semantic search on its own.

## Step two: connect your AI

Pick your agent. You need the address from step one, `http://127.0.0.1:27200/mcp`, and your token.

### Claude Code

One command in your terminal:

```
claude mcp add --transport http obsidian http://127.0.0.1:27200/mcp --header "Authorization: Bearer YOUR_TOKEN"
```

Replace `YOUR_TOKEN` with the token you made. Add `--scope user` on the end if you want the vault available in every project rather than just the current folder. Claude Code stores this in `~/.claude.json` and connects over plain HTTP with nothing else to install. Run `claude mcp list` to confirm it shows as connected.

### Codex CLI

Open `~/.codex/config.toml` and add this block:

```toml
[mcp_servers.obsidian]
url = "http://127.0.0.1:27200/mcp"
bearer_token_env_var = "OBSIDIAN_TOKEN"
```

Codex reads the token from an environment variable, so set `OBSIDIAN_TOKEN` to your token in your shell rather than writing the token into the file. Codex speaks HTTP directly, so no bridge is needed.

### Gemini CLI

Open `~/.gemini/settings.json` and add your server under `mcpServers`:

```json
{
  "mcpServers": {
    "obsidian": {
      "httpUrl": "http://127.0.0.1:27200/mcp",
      "headers": { "Authorization": "Bearer YOUR_TOKEN" }
    }
  }
}
```

Gemini uses `httpUrl` for this kind of connection. Its plain `url` field means something else.

### Cursor

Open `~/.cursor/mcp.json` (or a project-local `.cursor/mcp.json`) and add:

```json
{
  "mcpServers": {
    "obsidian": {
      "url": "http://127.0.0.1:27200/mcp",
      "headers": { "Authorization": "Bearer YOUR_TOKEN" }
    }
  }
}
```

### Other agents, including ones you run on open models

Cline, Continue, Goose, and opencode all speak MCP too, and they are the ones people most often point at a self-hosted or open-weight model. The vault side does not change; you register the same address and token in each one's own config. The exact field name is the only thing that drifts between them, so check the client's own MCP docs for the current syntax, since these tools change often. Two known quirks: Goose calls the address field `uri` instead of `url`, and opencode marks an HTTP server with `"type": "remote"`.

Here is the rule that tells you which shape a client wants. If its config takes a web address (a field like `url`, `httpUrl`, or `uri`), connect straight to the address above. If its config only takes a command to launch (fields like `command` and `args`), it speaks the older local style and needs a small bridge in between:

```
npx mcp-remote http://127.0.0.1:27200/mcp --header "Authorization: Bearer YOUR_TOKEN"
```

Pin `mcp-remote@0.1.16` or newer; older versions had a security hole. On Windows, `mcp-remote` can hang for a minute on connect, and the MCP Connector plugin bundles a small Python bridge script to get around that. You only need any of this for the launch-a-command style clients. The direct-address clients above, Claude Code included, skip it entirely.

## Check that it worked

Start your agent and ask it to list the files in your vault, or to read one note by name. If it hands back real content, you are wired. If it cannot connect, work down this list:

- Obsidian has to be running, with the MCP Connector plugin on. The server lives inside the app.
- A wrong or expired token gives an authorization error. Recopy it from the plugin's Access control panel.
- If the port was busy, your live address may not be 27200. Check the plugin settings for the real one and update your agent's config to match.
- Very large notes stop at about 100 KB on a full read. The agent can still read them in parts, and it will tell you when it needs to.

## An alternative for Claude users

Obsidian now ships its own official command-line tool, and Obsidian's team publishes a set of Agent Skills at [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) that teach Claude to drive it. That is a second, skills-based path that does not use the MCP server at all. Most people should use the MCP connection above, since it is the one that works across every agent. Keep the Skills route in mind if you are on Claude and want to lean on Obsidian's own tooling.

## What this does not cover

This guide gets your vault and your AI talking. It does not set up the Chief of Staff system that lives inside the vault. For that, once the connection works, follow [`SETUP-HUMANS.md`](SETUP-HUMANS.md), or hand [`SETUP-AI.md`](SETUP-AI.md) to your agent and let it build the system with you while you watch.
