---
name: paperclip-setup
description: Install Paperclip locally on Faizan's Windows machine, connect the Claude Code adapter (claude_local) using his Claude Pro login, and create the "LinkedIn Brand Studio" company with its 3 agents. Use when Faizan says "paperclip setup", "paperclip install", "paperclip chalu karo", or asks to add, repair or re-check the Paperclip installation.
---

# Paperclip Setup

Goal: get Paperclip running at http://localhost:3100 with Claude Code as the agent runtime, then build the LinkedIn team from `context/team.md`.

Follow `.claude/rules/paperclip-usage.md` throughout. Explain each concept in one or two simple lines as you go (Faizan is new to Paperclip). Verified facts and commands live in `references/paperclip/setup-notes.md`. Update that file whenever you confirm something new, and re-check the official docs (docs.paperclip.ing) if a step fails.

## Step 0: Check prerequisites
Run these and report a table of ✅/❌:
- `node --version` must be 24.11 or newer
- `python --version` must be Python 3 (needed for Claude subscription sign-in)
- `claude --version` must show the Claude Code CLI on PATH. The VS Code extension's bundled copy does not count.
- `ls ~/.paperclip` shows whether Paperclip is already installed

If something is missing, fix it before continuing:
- Claude CLI: `npm install -g @anthropic-ai/claude-code`
- Node too old: ask Faizan to install the latest Node 24 LTS from nodejs.org

## Step 1: Log in to the Claude CLI (Faizan does this)
The adapter needs a logged-in CLI. Ask Faizan to type `! claude` in the Claude Code prompt (or run `claude` in a terminal), complete the browser login with his Claude Pro account, and then exit. Do not use an API key unless he asks for one, because the API is billed separately from Pro.

## Step 2: Install and onboard Paperclip
```
npx paperclipai@latest onboard --yes
```
- Uses the default loopback mode only. Do not pass `--bind lan` or `--bind tailnet`.
- Data goes to `~/.paperclip`. Rerunning keeps the existing config, and `npx paperclipai configure` edits it.
- If you get an npm E404: `npx --registry https://registry.npmjs.org paperclipai@latest onboard --yes`
- Start later with `npx paperclipai run`, run in the background. Check that http://localhost:3100 responds.

## Step 3: Create the company (in the dashboard, with Faizan)
- Name: **LinkedIn Brand Studio**
- Goal: "Grow Faizan Akhtar's LinkedIn from 620 to 3,000+ followers by June 2027 with 2 to 3 original, human-sounding posts a week on AI automation (AI does the boring 80%, humans the 20%), so he gets inbound job offers in India."

## Step 4: Hire the agents (adapter: Claude Code / `claude_local`)
**Windows gotchas (verified 2026-10-17):** start the server with claude-code\bin first in PATH (`Paperclip-Start-Steps.txt`), or the hello probe fails; give every project a primary workspace. The exact API calls are in the `paperclip-continue` skill.

For every agent:
- `cwd`: `D:\Workflow_Agent_Tool\PaperClip\paperclip-workspace` (a dedicated folder, because Paperclip runs Claude in full-auto mode)
- `engine`: `cli` (ACP breaks on the space in the username)
- `maxTurnsPerRun`: 30 (the wizard default is 1000), to protect the Pro quota
- `heartbeat.maxConcurrentRuns`: 1 (the default is 20)
- Give each agent the LinkedIn writing rules (`.claude/rules/linkedin-writing.md`) and the no-LinkedIn-automation rule

| Agent | Reports to | Heartbeat |
|---|---|---|
| Content Strategist (CEO) | Faizan | Weekly (Monday) |
| Trend Researcher | CEO | Weekly (Sunday) |
| Writer | CEO | On assignment only |

Set the company and agent budgets **before** you turn heartbeats on (Paperclip pauses agents at 100% of budget).

## Step 5: Test run
Assign one task: "Trend note + 1 post draft about building my LinkedIn team with Paperclip". Check that the output follows the writing rules. Save good drafts to `projects/linkedin-branding/drafts/`.

## After setup
- Tick the steps in `projects/paperclip-setup/README.md`
- Log key choices in `decisions/log.md`
- Tell Faizan in 3 or 4 lines what is running, what it will cost him in Pro usage, and what he does each week
