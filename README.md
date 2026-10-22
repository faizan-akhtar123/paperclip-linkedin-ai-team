# Paperclip LinkedIn AI Team

A personal AI assistant built with **Claude Code**, plus a 3 agent AI team in **[Paperclip](https://github.com/paperclipai/paperclip)** that does the research and drafting for my LinkedIn content. I review everything and do every LinkedIn action by hand.

I am Faizan Akhtar, a junior AI automation consultant. My focus is AI automation for boring, repetitive work: AI handles the 80 percent, a human does the important 20 percent. This repo is that idea applied to my own LinkedIn.

## How it works

```
Trend Researcher  ──>  Content Strategist  ──>  Writer  ──>  Claude Code  ──>  Me
(what is trending)     (plans 2 to 3 posts)     (drafts)     (checks facts,     (reviews,
                                                              makes carousel)    posts by hand)
```

| Part | Runs on | Job |
|---|---|---|
| Content Strategist (CEO) | Paperclip, Claude Opus | Plans the week's posts, checks tone and rules |
| Trend Researcher | Paperclip, Claude Sonnet | Finds trends in AI automation, Claude and agents, with sources |
| Writer | Paperclip, Claude Sonnet | Drafts posts in my voice from real facts only |
| Claude Code assistant | Claude Code | Setup, skills, fact checks, pencil sketch carousels, engagement lists |

### Rules the team follows
- **Agents only draft.** They never post, like, comment, connect or message on LinkedIn. Automating LinkedIn breaks its terms.
- **Human review point.** Every draft is checked by me before it goes out. It has already caught a real mistake: an agent presented an untested project as proven experience.
- **Real facts only.** Agents read one facts file and may not invent numbers, dates or stories.
- **Small and cheap.** Runs on a Claude Pro plan: 3 agents, no automatic heartbeats until budgets are set, Sonnet for the routine jobs. One Writer run is about 25k input tokens.
- **Locked permissions.** Agents cannot create other agents or assign tasks.

## What is in this repo

| Path | What it is |
|---|---|
| `CLAUDE.md` | The assistant's main instructions |
| `.claude/skills/` | Claude Code skills: `paperclip-setup`, `paperclip-continue`, `daily-engagement-list`, `skool-post`, `session-close` |
| `.claude/agents/linkedin-scout.md` | A read only subagent that scouts LinkedIn posts (no click tools) |
| `.claude/rules/` | Writing rules, communication style, Paperclip usage rules |
| `references/paperclip/` | Verified Paperclip setup notes for Windows, including fixes for real problems |
| `references/examples/` | Style references for posts and engagement |
| `decisions/log.md` | Append only log of every meaningful decision and why |
| `projects/` | Workstreams: Paperclip setup, LinkedIn posts (published, drafts, carousels), Skool learning journal |
| `templates/` | Session summary template |

## Things I learned the hard way (Windows)

- **A space in the Windows username breaks the Claude Code adapter.** Paperclip launches `claude.cmd` through `cmd.exe`, which splits the path at the space. Fix: put the folder with the native `claude.exe` first in PATH before starting Paperclip (see `references/paperclip/setup-notes.md`).
- **A failed probe marks the AI connection `needs_attention`,** and then agent updates are refused. Reconnect it in the dashboard.
- **The dashboard can show "connected" while the login token is revoked.** The run fails in seconds with 0 tokens used. Reconnect, then clear the agent error and wake it again.
- **Every Paperclip project needs a primary workspace that is a git repo,** otherwise files land in the wrong place or runs fail.
- **A global SessionStart hook runs inside every agent run** and spends quota. Make it skip when `PAPERCLIP_AGENT_ID` is set.

More detail in `references/paperclip/setup-notes.md`.

## LinkedIn carousels

Every post ships with a pencil sketch carousel: an HTML file with SVG pencil filters, rendered slide by slide with headless Edge into 1080 x 1080 PNGs, then joined into one light PDF. See `projects/linkedin-branding/drafts/*-carousel.html`.

## What is not in this repo

Personal data stays on my machine: context files (background, income, goals), session logs, the facts file with company names, engagement lists with other people's names, LinkedIn analytics, login tokens and the agents' working folder. `CLAUDE.md` still references the `context/` files; to reuse this setup, create your own.

## Status

- Paperclip installed and connected to Claude Code
- 3 agents hired and tested (Researcher trend note, Writer post draft)
- Next: weekly flow with budgets, then an Analyst agent after 4 to 6 weeks of posting data

## Contact

Open to full time, part time and freelance work in AI automation, AI operations and business process automation. If you have a boring, repetitive task to automate, get in touch on LinkedIn.
