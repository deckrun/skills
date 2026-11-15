# Deckrun skills

The Deckrun skill teaches AI coding agents to deploy and operate apps with [Deckrun](https://deckrun.com) through the `deck` CLI: install it, sign in through the browser, create a cluster after your explicit yes, deploy, and diagnose failures. It never asks you to paste a token into the chat and never runs destructive commands.

The skill is deliberately thin: it tells the agent to run `deck agent-guide`, which ships with the CLI and always matches your installed version.

## Install

### Claude Code

Run these in Claude Code one at a time, each as its own message:

```
/plugin marketplace add deckrun/skills
```

```
/plugin install deckrun@deckrun-skills
```

The skill loads in your next session.

### Codex

Run this in Codex, which picks the skill up in the same session:

```
$skill-installer install https://github.com/deckrun/skills/tree/main/skills/deckrun
```

### Cursor

Run this in your terminal (it needs Node). Cursor loads the skill in your next chat.

```bash
npx skills add deckrun/skills -a cursor -g
```

### Any agent that supports Agent Skills

```bash
npx skills add deckrun/skills
```

Or copy `skills/deckrun/` into your agent's skills directory, for example `~/.claude/skills/deckrun/` for Claude Code or `~/.agents/skills/deckrun/` for Codex.

The setup pages at [deckrun.com/agents](https://deckrun.com/agents) have the same commands, and a prompt your agent can follow to install deck and the skill for you.

## Use

Ask your agent, for example:

- "Deploy this repo to my DigitalOcean with Deckrun"
- "My last deploy of web failed. Can you figure out why and fix it?"
- "How much CPU and memory is my app using on Deckrun?"

The agent will need you to:
- approve the sign-in in your browser;
- run `deck providers add` in your own terminal, so your cloud token never goes through the chat;
- confirm before it creates a cluster, since that creates billable resources in your cloud account.

## What it runs and what it sends

The skill is instructions only: it has no scripts, hooks or MCP servers, and it collects and sends nothing itself. It tells the agent to:

- run `deck` commands in your shell;
- install deck with Homebrew (`brew install deckrun/deck-cli/deck`) if it is missing. Without Homebrew, it asks you to install deck yourself;
- run `deck agent-guide`, which prints the usage guide built into your installed deck (it is not fetched from the network);
- sign you in with `deck auth login`, which opens `app.deckrun.com` in your browser, where you approve access. deck stores the token on your machine.

deck talks to the Deckrun API (`api.deckrun.com`) and to your cluster. It sends what the commands need: your app's configuration and container images, secrets you set, and the commands you approve. Your cloud provider token goes to Deckrun only when you run `deck providers add` yourself. See the [privacy policy](https://deckrun.com/privacy).

## Docs

- [Use deck with AI agents](https://deckrun.com/docs/getting-started/ai-agents)
- [Install Deck CLI](https://deckrun.com/docs/getting-started/install-deck-cli)

## License

MIT
