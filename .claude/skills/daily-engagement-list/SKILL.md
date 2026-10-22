---
name: daily-engagement-list
description: Faizan's daily LinkedIn engagement list. A Sonnet scout reads LinkedIn posts from the last 24 hours, then 3 active posts (20+ reactions or 5+ comments) on AI automation are picked, Indian authors first, each with a 1 to 2 line comment draft, plus India job leads. Faizan comments by hand. Use when Faizan says "engagement list", "aaj ke comments", "comment ke liye posts do", "daily engagement", or asks which posts to comment on today.
---

# Daily engagement list

Goal: 3 posts a day where a short, sharp comment from Faizan gets seen by the right people (India, AI automation, recruiters). About 7 minutes of his time.

**Hard rule:** never click, like, comment, follow or connect on LinkedIn. Only read and draft. Faizan does every LinkedIn action himself.

## Principle: intentional, not just active (added 2026-10-22)
Based on a LinkedIn post Faizan liked: "5 conversations with the right buyers beat 50 with people who will never buy." For Faizan the "buyers" are two groups, in this order:
1. **People who can hire him in India** (main goal): founders, hiring managers and recruiters at AI or automation companies.
2. **People who could later buy his services as a freelancer**: founders and owners of small and mid businesses with repetitive manual work (operations, sales, admin).
Also fine: AI automation creators whose audience is either group.
- **Right person first.** Every pick needs a one line "Kyun yeh sahi insaan hai" (who the author is, which buyer group they belong to: hiring or freelance, and why their audience matters). A big post from the wrong audience loses to a smaller one from the right audience.
- **No viral posts and no random CEOs** (removed 2026-10-22 on Faizan's call). Reach from the wrong audience does not count. Full base post: `references/examples/intentional-engagement-post.md`.
- **Follow up beats new.** People who replied to his comments are worth more than new authors (Step 1b).
- **Note 1 real problem a day.** One real problem seen in today's posts becomes a content idea (Step 4b).
- Time budget stays about 10 minutes a day. Job search comes first.

## Step 0. Result tracker (30 seconds)
Open `projects/linkedin-branding/engagement/log.md`. For rows dated 2 or more days ago with result `pending`, ask Faizan in one line per row: "Reply mila? (yes / no)". Write the answer in the Result column. Every 2 weeks, summarise in 2 lines which post types got replies.

## Step 1. Scout (Sonnet subagent)
Launch the `linkedin-scout` subagent (foreground) with: "Run today's scout." Before that, check that Faizan's Chrome is open with LinkedIn logged in; if the scout reports a login screen, ask him to log in and stop.

## Step 1b. Follow ups (up to 2)
From `log.md`, take rows with Result `yes` (the author or someone replied) from the last 14 days. For up to 2 of them, draft one next step for Faizan to do by hand: a 1 line reply back in that thread, or a short connection note (1 to 2 lines, mention the thread, no pitch, no asking for a job). Mark it in the daily file. If there are none, skip this step silently.

## Step 2. Pick 3 posts
From the scout table, keep only:
- Type `discussion`
- **20+ reactions or 5+ comments** (drop "unclear" unless nothing else is left, and then say so)
- Topic fits: AI automation, AI agents, Claude, operations, process improvement, AI careers
- Author not already used in the last 7 days of `log.md`

Then rank: right person first (hiring group before freelance group, see the Principle), then India signal "yes", then higher comments, then fresher.
Pick **3**, plus 1 new post for every empty follow up slot from Step 1b, so the day always has **5** (Faizan's call, 2026-10-22). If the first scout cannot fill 5, run the scout again with new keywords before giving up. Ideally 2 medium posts (20 to 200 reactions) plus 1 bigger or very active one. Prefer posts under 3 days old; older posts only if the discussion is still active. If a slot cannot be filled, say so honestly instead of lowering the bar silently.

Only pick rows where the scout's buyer group is `hiring` or `freelance` (or an AI automation creator whose audience is one of them). Skip `other`, even when the post is big.

## Step 3. Draft comments (main model, not the scout)
**Write each comment from the full post text the scout returned, never from the one line summary.** If a pick has no post text, drop it and take the next post. The comment must answer the post's actual point or question.
Follow `.claude/rules/linkedin-writing.md`:
- **Address the author by first name** so it reads like Faizan is talking to them (e.g. "Pawan, ...", "Agreed, Pawan.", "Good question, Esraa."). Vary the opener every time; never the same pattern twice in one list.
- **1 to 2 lines, one point.** English, human. No emojis, no dashes, no hashtags, no "Great post" or "Thanks for sharing".
- Add something: his real experience, an extra point, or a genuine question. Agreeing alone is not enough.
- Use only facts from `context/me.md` and `projects/linkedin-branding/project-facts.md` (Dubai HVAC/MEP coordination, job search agent, the Paperclip AI team for LinkedIn, the 80/20 view). **Never use the client acquisition system as an example**, it has never been run. Never invent numbers or stories.
- Do not name his employers or the companies he applied to.

## Step 4. India job leads
From scout rows of type `hiring` with India signal "yes", list up to 3 that fit an entry level AI automation, AI operations, junior AI consultant or business analyst profile. Skip senior roles (5+ years, lead, architect, principal). These are for applying, not commenting.

## Step 4b. Problem of the day
From today's posts and comments, note 1 real problem people describe (a manual task, a hiring pain, an AI tool failing). Append one line to `projects/linkedin-branding/engagement/problems.md` (create it if missing): `YYYY-MM-DD | problem | where seen | possible post angle`. Only what the post actually says, no guessing.

## Step 5. Save
1. Write `projects/linkedin-branding/engagement/YYYY-MM-DD.md` (template below).
2. Append one row per picked post to `projects/linkedin-branding/engagement/log.md` with Result `pending`.

## Step 6. Show Faizan
For each of the 3 posts, show all of this:
1. **Author** and their **LinkedIn headline** (full, from the scout), plus **Kyun yeh sahi insaan hai** in one line
2. **Post:** the full post text in a quote block, so Faizan knows exactly which post it is
3. **Matlab:** what the post says, 1 to 2 lines in simple Hinglish
4. Reactions / comments, and the **name search link** (`https://www.linkedin.com/search/results/content/?keywords=<Author%20Name%20+%201%20topic%20word>&datePosted=%22past-week%22`, because the topic search order shuffles), plus the topic search link as backup
5. **Comment to post** in a quote block, and one line on why this comment fits
Then the follow ups (if any), the problem of the day in one line, and the job leads in a small table. End with: "Comment post karna tumhara kaam hai. 2 din baad result puchunga."

## Daily file template
```
# Engagement list YYYY-MM-DD

| # | Author | Headline | Right person? | India | Reactions | Comments | Why this post | Name search link |
|---|---|---|---|---|---|---|---|---|

## Follow ups
(up to 2, from log.md rows with Result yes)

## Posts and comments
### 1. Author
Post: (full text)
Comment: ...
### 2. ...
### 3. ...

## Problem of the day
(1 line, also appended to problems.md)

## India job leads
| Company / poster | Role | Location | Search link |
|---|---|---|---|
```
