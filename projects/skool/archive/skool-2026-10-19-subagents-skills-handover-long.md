# Skool draft: backups, one skill for many agents, and a handover file

_Status: DRAFT_

---

What I learned today: cheap subagents, one skill for many agents, and a handover file

Today was a Claude Code and Paperclip day. I picked up a few small habits that make the setup safer. Here they are, plus one thing that confused me.

What I learned

1. A subagent can run on a cheaper model.
A subagent is a helper Claude starts for one job. In its file you can set the model, so I gave a reading job to Haiku, the cheaper model, and kept the stronger model for judgement. I also gave it only read tools, so it cannot click anything. Takeaway: cheap model for volume, strong model for decisions, and only the tools the job needs.

2. One skill can serve many agents.
A skill is a folder with one SKILL.md file that holds the rules and steps in plain text. I wrote my writing rules once as a skill, imported it into Paperclip, and attached it to one of my agents. The skill points to one facts file, so the agent always reads the current version. Takeaway: write the rules once, then attach them to every agent that needs them.

3. A closing skill writes a handover file.
My session close skill updates the READMEs, the decision log and the memory notes, then writes a session log. The description at the top of a skill tells Claude when to use it, so I only have to say "session close". Takeaway: end each session by writing down what got done, what was decided and what is still open.

What confused me

I edited my skill file, but my Paperclip agent still had the old version. Paperclip keeps its own copy when you import a skill, so I had to import it again. Lesson: after editing a skill, check that every place using it got the update.

What I want to learn next

Paperclip heartbeats. A heartbeat is a scheduled run that lets an agent work without me starting it. My plan is to set a budget for each agent before I schedule any heartbeat, so one agent cannot use up my Pro plan limit. I also want to test each new agent with one small task before I add the next one.

Question for you: in your own setup, where do you draw the line between a cheap model and a stronger one, and how do you decide?

---

**Note for Faizan (not part of the post)**

- **Log items used:** settings backup before the hook edit (global neck-stretch hook, session log); voice skill imported into Paperclip and attached to the Content Strategist, reading the facts file; session close skill (READMEs, decision log, memory, then session log); Paperclip heartbeats and budgets before scheduling (next steps in the log and the Paperclip usage rules).
- **Left out on purpose:** the LinkedIn direct links script, the engagement list, the scout agent and everything about posts or comments. Also the backup file path and the skill key ID.
- **Check before posting:**
  - The "What confused me" section is my reading of the log, not a line you wrote. The log shows you imported the skill into Paperclip, but not that you were confused. Edit it if it does not match what you felt.
  - "Heartbeat" is explained from the Paperclip usage rules. Confirm the meaning is right before you post it.
  - The lesson about the hook being global repeats the earlier Skool draft, so I did not use it as a lesson here.
- **Word count:** 399 words including the title (within 200 to 400).
