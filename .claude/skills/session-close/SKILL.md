---
name: session-close
description: Close out Faizan's work session. Writes a session log (what got done, decisions, what is pending) from templates/session-summary.md into sessions/YYYY-MM-DD-session-summary.md and makes sure READMEs, decision log and memory are current. Use when Faizan says "session close karo", "session khatam", "log karo kya hua", "aaj ka summary", "wrap up", or asks to record what was done and what is left.
---

# Session close

Goal: one file that tells the next session exactly where things stand, so Faizan never has to re-explain.

## Step 1. Gather (from this conversation, do not invent)
- What got done (files created or changed, posts published, comments made, Paperclip changes).
- Decisions made this session.
- New preferences Faizan gave.
- What is still pending: read the "Pending" sections of `projects/paperclip-setup/README.md` and `projects/linkedin-branding/README.md`, plus `projects/linkedin-branding/engagement/log.md` rows marked `pending`.

## Step 2. Make sure the sources are current
Before writing the log, fix anything this session forgot:
- Tick finished items and add new ones in the project READMEs.
- Append missing decisions to `decisions/log.md` (append only, format `[YYYY-MM-DD] DECISION: ... | REASONING: ... | CONTEXT: ...`).
- Save new preferences as memory; update the `paperclip-setup-progress` memory if Paperclip changed.
- If a priority shifted, update `context/current-priorities.md`.

## Step 3. Write the log
Use `templates/session-summary.md`. Save as `sessions/YYYY-MM-DD-session-summary.md` (today's date). If that file already exists, add a new section `## Later session (HH:MM)` instead of overwriting.
- **What Got Done:** short bullets with file paths.
- **Decisions Made:** one line each, pointing to `decisions/log.md`.
- **Open Items / Next Steps:** a table `When | Task | Who`, job search first, then LinkedIn, then Paperclip (P numbers).
- **Memory Updates:** names of memories added or changed.

## Step 4. Tell Faizan (short, Hinglish ok)
Link to the log, then 3 to 5 bullets: done, and the top pending items in order. Remind him: job search first next time.
