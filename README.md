# Deckrun skills

The Deckrun skill teaches AI coding agents to deploy and operate apps with [Deckrun](https://deckrun.com) through the `deck` CLI: install it, sign in through the browser, create a cluster after your explicit yes, deploy, and diagnose failures. It never asks you to paste a token into the chat and never runs destructive commands.

The skill is deliberately thin: it tells the agent to run `deck agent-guide`, which ships with the CLI and always matches your installed version.

## Install

### Claude Code

```
/plugin marketplace add deckrun/skills
/plugin install deckrun@deckrun-skills
```

### Any agent that supports Agent Skills

```bash
npx skills add deckrun/skills
```

Or copy `skills/deckrun/` into your agent's skills directory, for example `~/.claude/skills/deckrun/` for Claude Code or `~/.agents/skills/deckrun/` for Codex.

## Use

Ask your agent, for example: "Deploy this repo to my DigitalOcean with Deckrun".

The agent will need you to:
- approve the sign-in in your browser;
- run `deck providers add` in your own terminal, so your cloud token never goes through the chat;
- confirm before it creates a cluster, since that creates billable resources in your cloud account.

## Docs

- [Use deck with AI agents](https://deckrun.com/docs/getting-started/ai-agents)
- [Install Deck CLI](https://deckrun.com/docs/getting-started/install-deck-cli)

## License

MIT
