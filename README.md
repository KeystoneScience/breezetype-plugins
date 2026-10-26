# BreezeType plugins for Claude and ChatGPT

Search your [BreezeType](https://breezetype.com) dictations, meetings and Ambient Notes from Claude Code, Codex and the ChatGPT desktop app.

The plugin connects your AI app to the MCP server built into the BreezeType Mac app. It reads your BreezeType data on your Mac, and nothing goes through a BreezeType server. The AI app you connect sends what it reads to its own model provider, as it does with anything else you share with it.

## What your AI app can do

- **Dictations:** search everything you've dictated, by text, app or website.
- **Meetings:** search notes, summaries, participants and transcripts, and read a full transcript.
- **Ambient Notes:** search the transcripts of your Ambient Notes sessions.
- **Clipboard:** search recent clipboard items.
- **Suggest meeting edits:** propose a meeting note or a new summary. BreezeType shows it in that meeting for you to approve. Nothing changes until you approve it.

It can't delete anything, publish anything, or apply its own suggestions.

You choose what agents can read on BreezeType's **Agents** page (BreezeType 0.1.13 or later): dictation history, clipboard history, meetings and Ambient Notes. Ambient Notes are off by default; the others are on.

## Requirements

- A Mac with [BreezeType](https://breezetype.com) installed in Applications. Open it once before connecting.

## Easiest: connect from BreezeType

In BreezeType 0.1.13 or later, open **Agents** in the sidebar and click **Connect** next to Claude or ChatGPT. Then quit and reopen that app.

For Claude Code, click **Copy prompt** and paste it into Claude Code.

## Claude Code

```sh
claude plugin marketplace add KeystoneScience/breezetype-plugins
claude plugin install breezetype@breezetype
```

Restart Claude Code. To remove it:

```sh
claude plugin uninstall breezetype@breezetype
```

## Codex and the ChatGPT desktop app

```sh
codex plugin marketplace add KeystoneScience/breezetype-plugins
codex plugin add breezetype@breezetype
```

Restart the app. In the ChatGPT desktop app, the plugin is also listed in the Plugins Directory under the BreezeType marketplace.

## Any other MCP app

Add a local (stdio) server named `breezetype` that runs BreezeType's launcher with no arguments:

```json
{
  "mcpServers": {
    "breezetype": {
      "command": "/Applications/BreezeType.app/Contents/Resources/resources/scripts/mcp/breeze-mcp",
      "args": []
    }
  }
}
```

## Troubleshooting

- **"BreezeType is not installed":** the plugin looks for BreezeType in `/Applications`, then in `~/Applications`, then anywhere Spotlight can find it. Install BreezeType, open it once, then restart your AI app.
- **A tool says access is off:** turn that source on (Dictation history, Clipboard history, Meetings or Ambient Notes) on BreezeType's Agents page.
- **Results look out of date:** the clipboard tools only see items copied while BreezeType was running.

## What's in this repository

| Path | Purpose |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code marketplace |
| `.agents/plugins/marketplace.json` | Codex and ChatGPT marketplace |
| `plugins/breezetype/.mcp.json` | Starts BreezeType's MCP server on this Mac |
| `plugins/breezetype/skills/breezetype/SKILL.md` | Tells the AI how to use the tools well |

The MCP server itself ships inside the BreezeType app. This repository has no code that reads your data.

## License

MIT
