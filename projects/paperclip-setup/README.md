# Paperclip Setup

Install Paperclip locally and connect it to Claude Code as the agent runtime.

- **Status:** Active. 2 of 3 agents hired (Content Strategist, Trend Researcher). Last updated 2026-10-20.
- **Deadline:** Before 26 Nov 2026 (ideally within 2 weeks)
- **Ready:** Node.js v24, npm, git, Claude Code (Pro plan)
- **Daily start:** `Paperclip-Start-Steps.txt` (project root). The PATH line is required every time.

## Steps
1. [x] Read the official docs and repo (github.com/paperclipai/paperclip). Save notes in `references/paperclip/`.
2. [x] Install and start the local server and dashboard.
3. [x] Connect the Claude Code adapter. The hello probe failed because of the space in the username; it passes with claude.exe first in PATH.
4. [~] Create the company "LinkedIn Brand Studio" with 3 agents (see `context/team.md`). The Content Strategist is hired; the Trend Researcher and Writer are not yet.
5. [~] Low limits to fit the Pro plan. The Strategist is done: engine CLI, maxTurnsPerRun 30, maxConcurrentRuns 1, heartbeat off. Budgets are not set yet.
6. [x] Test run. The Strategist produced 3 post ideas (2026-10-17), and post 1 was published.

## Pending tasks (in order)
Used by the `paperclip-continue` skill. Tick an item when it is done, and add new items at the end.

- [x] **P1. Build the `faizan-linkedin-voice` skill** (done 2026-10-19: `paperclip-workspace/skills/faizan-linkedin-voice/`, imported as company skill `local/c5bbdb33c8/faizan-linkedin-voice`, attached to the Strategist; attach to the Writer at hire) (Paperclip skill for the Strategist and Writer): profile, positioning, `.claude/rules/linkedin-writing.md`, `projects/linkedin-branding/project-facts.md`, and the .md + .txt output format.
- [x] **P2. Hire the Trend Researcher** (test run done 2026-10-21: issue LIN-2 in project "LinkedIn Content", note `paperclip-workspace/research/trend-note-2026-10-21.md`, facts check passed, ran on Opus, about 172k input tokens) (hired 2026-10-20: id `901009d5-772f-463b-9818-d2d768aa366c`, reports to the Strategist, same limits, skills `trend-research` (`local/46a8b74915/trend-research`, source `paperclip-workspace/skills/trend-research/`) + voice skill, canCreateAgents and canAssignTasks off).
- [x] **P3. Hire the Writer** (test run done 2026-10-22: LIN-3, Sonnet, about 25k input + 3k output tokens, post 04 draft passed the rules check, hook reworded by Claude Code for accuracy) (hired 2026-10-21: id `68192aac-c859-47e5-9448-2e298bb93715`, Sonnet 5.5, reports to the Strategist, voice skill, heartbeat off, canCreateAgents and canAssignTasks off. **Still open:** test run on 22 Oct after P9, as an issue in project "LinkedIn Content"; Claude makes the carousel. Trend 1 angle in the note uses the client acquisition system: replace it with the Paperclip team, never use client acquisition as an example) (reports to the Strategist), on assignment only. Test run: 1 full post draft (.md + .txt) from the Researcher's trend and one idea from `drafts/post-ideas-week1.md`.
- [ ] **P4. Weekly flow:** Researcher on Sunday, Strategist plan on Monday, Writer drafts 2 to 3 posts. Set the company and agent budgets **before** turning heartbeats on.
- [x] **P5. Quota guard:** (done 2026-10-19: hook now starts with `[ -n "$PAPERCLIP_AGENT_ID" ] ||`, backup `settings.json.bak-2026-10-19`) make the global neck-stretch SessionStart hook skip non-interactive runs (it currently fires inside agent runs).
- [ ] **P6. Permanent PATH fix** (optional, needs Faizan's OK): add the claude-code\bin folder to the user PATH before %APPDATA%\npm.
- [x] **P7. Ask Faizan:** (done 2026-10-20: nothing was dropped; the system is built but untested and has sent no email, see project-facts.md) anything he tried to automate in client acquisition and then dropped (needed for post idea 3).
- [x] **P8. Pick the agent model to save quota:** (done 2026-10-21: Researcher `adapterConfig.model = "claude-sonnet-5-5"`; give the Writer the same at hire; Strategist stays on the default Opus for now) the Researcher test ran on Opus (about 172k input + 26k output tokens). Set Sonnet for the Researcher and Writer (needs Faizan's OK).
- [x] **P9. Answer the 5 [ASK FAIZAN] questions** (done 2026-10-22: trend 2 dropped, 43 applications, near miss = Researcher used client acquisition, move OK to post; answers at the end of the trend note) at the end of the trend note (2 minutes), so the Writer can draft from trend 1.

## Gotchas (details in `references/paperclip/setup-notes.md`)
- Start Paperclip without the PATH line and the probe fails; the AI connection then becomes `needs_attention`. Fix: restart with the PATH line, then go to `/LIN/apps/connections` and click Reconnect.
- Every new Paperclip project needs a primary workspace pointing to `paperclip-workspace`, otherwise files are saved under `~/.paperclip`.
