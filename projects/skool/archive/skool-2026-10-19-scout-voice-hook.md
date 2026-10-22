# Skool post: Build log, scout agent, voice skill and hook fix

_Status: DRAFT_

---

Build log: a scout agent, a shared voice skill and a hook fix

Today was a building day with Claude Code. Here is what I shipped, what I learned, and one thing that did not work. Some of it might save you time.

What I built

A daily engagement skill. It reads LinkedIn posts from the last 24 hours and picks three active posts on AI automation. A Haiku subagent does the scouting because it is cheap. Its tools are read only, with no click tool, so it cannot like, comment or post. The main model writes the short comment drafts, and I post them by hand.

A voice skill for my Paperclip agents. My writing rules and the only facts I am allowed to use live in one file, and the skill points to that file instead of copying the facts into every agent. When a fact changes, I edit one place.

A session close skill. It updates the READMEs, the decision log and the memory notes, then writes a session log. That log is what the next draft gets written from.

What I learned

Haiku is good for the high volume, boring part (reading and listing). Let the cheap model find things and let the stronger model judge them.

Give a subagent only the tools it needs. A scout with no click tool is safer than a scout you just trust to behave.

Keep facts in one file. Agents that copy facts drift apart fast.

Global hooks affect everything you run. My reminder hook was also running during Paperclip agent runs, so I made it skip those runs when an agent flag is set.

What did not work

I wanted direct post links inside the engagement list. Getting them meant running a script on the LinkedIn page, and I said no to that. For now I get the author name and the search page, and the links wait for a safer method.

What's next

A Trend Researcher agent for the weekly research, then a Writer agent, with budgets set before any scheduled runs. I am keeping the team small so it stays inside the Pro plan limit.

A reply check on the comments I posted today, to see which ones get answers.

Question for you: when you build a helper agent, do you give it write access, or only read tools, and why?

---

**Note for Faizan (not part of the post)**

- **Log items used:** daily engagement skill with the read only Haiku scout (no click tool); the main model writes comment drafts and you post by hand; the voice skill with facts in one file, attached to the Paperclip agent; the session close skill; the neck-stretch hook now skipping Paperclip agent runs; the declined script for direct post links; the P2 Trend Researcher and P3 Writer next steps; the reply check on the 19 Oct comments.
- **Check before posting:**
  - The hook line says "reminder hook". Change it if the hook has a different purpose.
  - "Pro plan limit" matches the team and budget notes in the context files.
  - The direct links line was clarified by Claude Code: you said no to running a script on the LinkedIn page.
- **Not in the log, so left out:** any claim about post results, and any comment about how comment length affects reach.
- **Word count:** about 330 words (within 200 to 400).
