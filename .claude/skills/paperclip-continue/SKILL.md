---
name: paperclip-continue
description: Resume Faizan's Paperclip work where it stopped. Checks that the Paperclip server is up with the PATH fix and that the Claude connection is healthy, shows the pending task list, and then does the next pending task (build a skill, hire the next agent, set up the weekly flow). Use when Faizan says "paperclip continue karo", "paperclip continue", "aage badho", "next task", "pending kya hai", or asks what to do next in Paperclip.
---

# Paperclip Continue

Goal: in a few minutes, confirm that Paperclip is healthy and then move the next pending task forward. Faizan's time cost should stay around 10 minutes.

Follow `.claude/rules/paperclip-usage.md` and `.claude/rules/communication-style.md` (Hinglish is fine, use tables, explain each Paperclip concept in one line).

## Fixed IDs
| What | Value |
|---|---|
| API base | `http://127.0.0.1:3100/api` |
| Company "LinkedIn Brand Studio" | `7bb228a5-ac4d-468c-a24b-05fa8460e108` (prefix LIN) |
| Content Strategist | `9e6c8461-9f5d-4378-b69c-6efea63813f8` |
| AI connection "My Claude subscription" | `7b58cbf4-c038-4b44-ac66-e1f477e67534` |
| Agent workspace | `D:\Workflow_Agent_Tool\PaperClip\paperclip-workspace` |

## Step 1: Health check (read-only, do it yourself)
1. **Server:** `GET /api/health` should return `status: ok`. If it is down, tell Faizan to follow `Paperclip-Start-Steps.txt` and wait.
2. **PATH fix active?** A server started without the PATH line makes every agent probe fail. Do **not** run a test just to check, because a failed probe marks the connection `needs_attention`. If unsure, ask Faizan whether he ran step 2 of `Paperclip-Start-Steps.txt` in that window.
3. **Connection:** `GET /api/companies/<company>/ai-connections`, where the status must be `connected`. If it shows `needs_attention`: (a) restart with the PATH line, (b) Faizan opens `http://localhost:3100/LIN/apps/connections`, clicks My Claude subscription, then Reconnect, and pastes the code into the terminal (never into chat).
4. **Agents:** `GET /api/companies/<company>/agents`. Report each agent's status; heartbeat must be off until P4.

Show the results as a short ✅/❌ table.

## Step 2: Show the pending list
Read the "Pending tasks" section of `projects/paperclip-setup/README.md` and the "Pending" section of `projects/linkedin-branding/README.md`. Show the open items and name the next one. If Faizan picks a different item, do that one.

## Step 3: Do the next task
Before anything that runs an agent, say roughly how much Pro quota it uses.

**Hiring an agent (P2, P3):**
- Hire in the dashboard with Faizan (wizard) or through the API, using the Claude subscription connection.
- Then `PATCH /api/agents/<id>` with `adapterConfig: { engine: "cli", maxTurnsPerRun: 30, cwd: <agent workspace> }` and `runtimeConfig` (copy the existing one and change only `heartbeat.maxConcurrentRuns = 1`, keeping `aiConnection`). PATCH runs a probe first, so the connection must be healthy.
- Set `reportsTo` to the Strategist.
- Do not pass `--dangerously-skip-permissions` in local test commands; the auto mode classifier blocks it.

**New Paperclip project:** add a primary workspace right away:
`POST /api/projects/<id>/workspaces` with `{"name":"PaperClip folder","sourceType":"local_path","cwd":"D:\\Workflow_Agent_Tool\\PaperClip\\paperclip-workspace","isPrimary":true}`.

**Giving an agent a task:** keep it small. Tell it not to create agents and not to post anywhere. Ask it to save the output to the workspace. Afterwards, check the output against `.claude/rules/linkedin-writing.md`, especially that it uses only facts from `projects/linkedin-branding/project-facts.md`. Copy good drafts to `projects/linkedin-branding/drafts/`, as .md plus a paste-ready .txt for final posts.

## Step 4: Close out
- Tick finished items in both READMEs and add any new pending items.
- Update `references/paperclip/setup-notes.md` with anything newly confirmed.
- Update the memory file `paperclip-setup-progress`.
- Log meaningful decisions in `decisions/log.md` (append only).
- Tell Faizan in 3 or 4 lines: what is done, what is next, and what he needs to do (in minutes). Job search always comes first; if he mentions pending assignments or interviews, remind him of those first.
