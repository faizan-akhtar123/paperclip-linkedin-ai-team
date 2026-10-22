# Paperclip Setup Notes (verified)

_Checked against the official repo and docs.paperclip.ing on 2026-10-16._

## Requirements
- Node.js **24.11.0 or newer** (this machine has 24.19 ✅)
- Python 3 for Claude subscription sign-in (this machine has 3.14.7 ✅)
- Claude Code CLI on PATH on the same machine
- Database: embedded PostgreSQL is created automatically. There is no separate install.

## Commands
| Task | Command |
|---|---|
| Install and onboard with defaults | `npx paperclipai@latest onboard --yes` |
| Persistent install | `npx paperclipai install` |
| Start the server | `paperclipai run` (or `npx paperclipai run`) |
| Edit the config | `npx paperclipai configure` |
| Background service status | `paperclipai service status` |
| Dashboard | http://localhost:3100 |

Data lives in `~/.paperclip` (config, database, logs, secrets).

## Claude Code adapter
- Type key: `claude_local` ("Claude Code", the recommended option)
- Auth: `ANTHROPIC_API_KEY`, Bedrock, **or a Claude subscription login**
- Fields: `cwd`, `model`, `promptTemplate`, `timeoutSec`, `graceSec`, `maxTurnsPerRun` (default 300), `dangerouslySkipPermissions` (default true: full auto)
- It resumes the session on the next heartbeat when `cwd` is unchanged.
- Paperclip skills are passed in through `--add-dir`.

## Cost note
The docs estimate $5 to 20 for experimenting and $20 to 100 a month for an active company **on the API**. With the Pro login, runs use the Pro usage limits instead, so keep heartbeats rare and `maxTurnsPerRun` low.

## Windows (tested on this machine, 2026-10-16)
- `npx --yes paperclipai@latest onboard --yes` works. Result: 11 checks passed, 1 warning.
- Warning: the `master.key` permissions are 666. `chmod 600` has no effect on Windows, so ignore it for local-only use.
- "Service management is not supported on win32", so Paperclip will not auto-start. Start it each time with `npx paperclipai run`.
- The first start applies about 300 database migrations, which takes about 1 minute.
- Instance home: `C:\Users\FAIZAN AKHTAR\.paperclip\instances\default\` (config.json, db on port 54329, hourly backups)
- Health check: http://127.0.0.1:3100/api/health
- The Claude CLI was installed with `npm install -g @anthropic-ai/claude-code` (v2.1.301). It is already logged in with the claude.ai account because it shares `~/.claude`.

## Docs
- Quickstart: https://docs.paperclip.ing/guides/getting-started/five-minute-path/
- Installation: https://docs.paperclip.ing/reference/cli/installation/
- Claude Code adapter: https://docs.paperclip.ing/reference/adapters/claude-code/
- Costs and budgets: https://docs.paperclip.ing/guides/day-to-day/costs/

## Company and Claude connection (2026-10-16)
- In the onboarding wizard, the "Claude Subscription" card runs `claude setup-token` itself. The browser asks for a code: paste it into the terminal window that shows the setup-token screen, not into a Claude chat.
- The result is an AI connection called "My Claude subscription" (API: `GET /api/companies/<id>/ai-connections`). Paperclip injects `CLAUDE_CODE_OAUTH_TOKEN` from it, which is why the test says "Detected in configured environment variables".
- The token can also be stored as a company secret without showing it in shell history:
  `$env:CLAUDE_CODE_OAUTH_TOKEN = (Read-Host "Paste token") -replace '\s',''` then
  `npx paperclipai secrets create --company-id <id> --name claude-oauth-token --value-env CLAUDE_CODE_OAUTH_TOKEN`, then remove the env var.
- To check that a token works on its own: set `CLAUDE_CODE_OAUTH_TOKEN` and an empty `CLAUDE_CONFIG_DIR`, then run `"Respond with hello." | claude --print`.
- Open issue: the agent Test fails with "Claude hello probe failed, exit code 1" even though the token works. Paperclip hides the probe's stderr (only "nonzero_exit" is logged). A real auth failure shows as "login required" instead. The default cwd is C:\WINDOWS\System32. Next steps: retry, then set engine=cli and a project cwd.
- The global SessionStart hook in `~/.claude/settings.json` used to run inside agent runs (fixed 2026-10-19, see "Agent run environment").

## Root cause of "hello probe failed, exit code 1" (found 2026-10-16)
- The Windows username has a space (`C:\Users\FAIZAN AKHTAR\...`). Paperclip resolves `claude` to `AppData\Roaming\npm\claude.cmd` and launches it as `cmd.exe /d /s /c "<quoted path>" ...` with `shell:false`. Node escapes the quotes as `\"`, so cmd sees `'\"C:\Users\FAIZAN AKHTAR\...\claude.cmd\"' is not recognized`. Reproduced outside Paperclip.
- Source: `@paperclipai/adapter-utils/dist/server-utils.js` (`resolveSpawnTarget`, `.cmd` branch).
- Fix: put `%APPDATA%\npm\node_modules\@anthropic-ai\claude-code\bin` (contains the native `claude.exe`) in PATH before `%APPDATA%\npm`. Paperclip then finds `claude.exe` and spawns it directly, so spaces are fine. Verified: direct spawn returns exit 0 and "Hello!".
- Quick, per-session version: in the terminal before `npx paperclipai run`:
  `$env:Path = "$env:APPDATA\npm\node_modules\@anthropic-ai\claude-code\bin;" + $env:Path`
- If a probe fails, the AI connection becomes `needs_attention` and agent PATCHes are refused. Fix: dashboard `/LIN/apps/connections`, then Reconnect.
- Agent files go to the **project workspace**, not the agent `cwd`. By default that is `~/.paperclip/instances/default/projects/<company>/<project>/_default`. To keep files in the PaperClip folder, add a primary workspace: `POST /api/projects/<id>/workspaces` with `{"name":"PaperClip folder","sourceType":"local_path","cwd":"D:\\Workflow_Agent_Tool\\PaperClip\\paperclip-workspace","isPrimary":true}`. Do this for every new project.
- (verified 2026-10-21) A project workspace must contain its own `.git` folder, or every issue run fails at once with "expected a git workspace for claude_local ... has no .git metadata" (`server/dist/services/heartbeat.js`, `hasGitMetadata`). Fix done: `git init` inside `paperclip-workspace` (the outer repo ignores that folder, so this nested repo is local only).
- To retry a failed issue run: `POST /api/agents/<id>/clear-error`, then `POST /api/agents/<id>/wakeup` with `{"source":"assignment","triggerDetail":"manual","payload":{"issueId":"<issue id>"}}` (verified 2026-10-21). Setting the issue back to `todo` does not wake the agent by itself. A wakeup with `failedRunId` is refused ("cannot override its execution context").
- (2026-10-21) The subscription token can get revoked between sessions (run error "OAuth token revoked"), and the connection then shows `needs_attention`. Fix: dashboard `/LIN/apps/connections`, then Reconnect.
- (verified 2026-10-21) Model per agent: `adapterConfig.model`. Blank means the default `claude-opus-5`. Sonnet 5.5 is `claude-sonnet-5-5` (needs Claude Code v2.1.284+). Send the full adapterConfig in the PATCH with only `model` added. Field list: `agentConfigurationDoc` in `@paperclipai/adapter-claude-local/dist/index.d.ts`.
- The ACP engine launches `claude-agent-acp.cmd` from the npx cache (also under the spaced path), so use engine = CLI for agents.

## Company skills (verified 2026-10-19, docs.paperclip.ing/reference/skills/)
- A skill is a folder with `SKILL.md` (frontmatter `name`, `description`). Installed per company, then attached per agent.
- Import: `POST /api/companies/<id>/skills/import` with `{"source":"D:/.../skills/<name>"}`. The path must be inside an approved root (a registered project workspace such as `paperclip-workspace`). Use forward slashes and send the body from a file (`--data-binary @file.json`); backslashes from Git Bash gave "Invalid JSON body".
- Attach: `POST /api/agents/<agentId>/skills/sync` with `{"mode":"add","desiredSkills":["<key>"]}`. `mode` is required (`add`, `remove`, `replace`); `replace` overwrites the whole list.
- Check: `GET /api/agents/<agentId>/skills`. A new skill shows `state: configured` and is materialized on the agent's next run.
- Our skill: `faizan-linkedin-voice`, key `local/c5bbdb33c8/faizan-linkedin-voice`. It points to `projects/linkedin-branding/project-facts.md` by absolute path, so facts stay in one place.

## Hiring an agent by API (verified 2026-10-20)
- `POST /api/companies/<id>/agents` with `name`, `role`, `reportsTo`, `adapterType: "claude_local"`, the full `adapterConfig` and `runtimeConfig` (copy the Strategist's), `budgetMonthlyCents`, and `desiredSkills` (skill keys). Creating does **not** run a probe, so put every setting in the create call and skip the PATCH.
- Use forward slashes in `cwd` (`D:/Workflow_Agent_Tool/PaperClip/paperclip-workspace`). Backslashes gave "Invalid JSON body" again, even though the JSON was valid.
- New agents get `canCreateAgents: true` by default. Turn it off: `PATCH /api/agents/<id>/permissions` with `{"canCreateAgents":false,"canAssignTasks":false}` (both fields are required).
- The `paperclipai/paperclip/paperclip` skill is added automatically.
- If the company requires board approval for new agents, use `POST /api/companies/<id>/agent-hires` instead.

## Agent run environment
- Paperclip sets `PAPERCLIP_AGENT_ID`, `PAPERCLIP_RUN_ID`, `PAPERCLIP_COMPANY_ID`, `PAPERCLIP_API_KEY` in every agent run. The global SessionStart hook now skips when `PAPERCLIP_AGENT_ID` is set, so agent runs no longer spend quota on the neck-stretch reminder.
- (seen 2026-10-21 and 2026-10-22) The subscription OAuth token gets revoked between days: the run fails in ~7 s with "OAuth token revoked", errorCode claude_auth_required, 0 tokens used, but GET ai-connections still shows `connected`. Fix: Reconnect in /LIN/apps/connections, then clear-error + wakeup. Cause not confirmed (guess: a fresh Claude login elsewhere rotates the token). Run details: GET /api/companies/<company>/heartbeat-runs?agentId=<id> or GET /api/issues/<id>/runs.
- (verified 2026-10-22) Writer test run LIN-3 on Sonnet 5.5: about 25k input + 3k output tokens for one post (the Researcher's first run on Opus used about 172k + 26k). Assigning an issue to an agent wakes it at once (invocationSource assignment), no manual wakeup needed.
