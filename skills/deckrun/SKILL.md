---
name: deckrun
description: Deploy and operate apps with Deckrun through the deck CLI. Use when the user wants to deploy an app to their own cloud (DigitalOcean or Scaleway) with Deckrun, create a Deckrun cluster, check why a Deckrun app or deploy is failing, read its logs, or set its secrets or domains; or when the repo has a deckrun.toml or a Deckrun section in AGENTS.md.
---

# Deckrun

Deckrun deploys apps to managed Kubernetes clusters that it creates in the user's own cloud account. You operate it only through the `deck` CLI. Never call the Deckrun API directly.

## 1. Make sure deck is installed

Run `deck version`.

- Not installed: install it with `brew install deckrun/deck-cli/deck` if Homebrew is available, otherwise `curl -L https://deckrun.com/install-cli.sh | sh`.
- Older than 2.1 (`deck agent-guide` is an unknown command): upgrade with `brew upgrade deck`, or run the install script again.

## 2. Read the guide

Run `deck agent-guide` and follow it. It matches the installed version and has the workflow, every command with its flags, and the JSON each one returns. Before writing `deckrun.toml` by hand, run `deck agent-guide config`.

## 3. Sign in

If a command fails with `unauthorized`, run `deck auth login --output json` in the background, show the user the URL from its first line, and wait for them to approve it in the browser.

## Rules

- Never run a destructive command (`deck apps delete`, `deck clusters delete`, `deck domains delete`, `deck providers delete`, `deck secrets unset`, `deck auth logout`), and never pass `--yes` to one. If the user wants one, give them the exact command from `deck agent-guide` to run in their own terminal.
- Before `deck clusters create`, tell the user the provider, region, node size and node count, say that it creates billable resources in their cloud account, and wait for an explicit yes.
- Before every `deck exec`, show the user the exact command and wait for their yes. Never open an interactive shell, and never print secret values (`env`, `printenv`). `deck forward` needs no confirmation.
- Never ask the user to paste a cloud provider token or a Deckrun token into the chat. The user runs `deck providers add` in their own terminal.
- If a step fails, stop and explain the error to the user instead of improvising.
