# LinkedIn Writing Rules

These apply to every LinkedIn post, comment or reply drafted for Faizan, whether by Claude Code or by a Paperclip agent.

## Voice
- English, professional, human. It must read like a person wrote it, not AI.
- First person, built on his real experience: his projects, Dubai site coordination, UK life, learning in public.
- Short paragraphs, a strong first line, one clear idea per post. End with a genuine question when it fits.
- **Fixed closing on every post** (Faizan, 2026-10-22): after the question and before the hashtags, add these two lines, each as its own paragraph, exactly:
  "I am looking for full time, part time and freelance opportunities in AI automation, AI operations and business process automation."
  "If you have any boring, repetitive task to automate, you can get in touch with me."
  Update the role words if his LinkedIn headline changes.

## Comments and replies
- Short and precise: 1 to 2 lines, one point. Never multi-paragraph.
- This covers the first comment on his own post, replies to comments, and comments on other people's posts.
- **Talk to the person by first name** in comments on other people's posts and in replies, so it reads like a conversation, not a broadcast. Work the name in naturally and vary it ("Pawan, ...", "Agreed, Pawan.", "Good question, Esraa.", "Elad, ..."), never the same opener every time. Use the first name as shown on their profile; for company pages, skip the name.

## Engagement strategy
Base: **intentional, not just active** (`references/examples/intentional-engagement-post.md`). 5 conversations with the right buyers beat 50 with people who will never buy.
- **Buyers, in this order:** 1. people who can hire Faizan in India (founders, hiring managers, recruiters at AI or automation companies); 2. business owners who could later buy his freelance AI automation services (small and mid businesses with repetitive manual work).
- **3 comments a day** on posts by those people, or by AI automation creators whose audience is those people. 20+ reactions or 5+ comments, Indian authors first. Right person beats a bigger post.
- **Up to 2 follow ups a day** with people who replied to him (a reply back, or a short connection note after a real exchange; no pitch, no asking for a job).
- **1 real problem a day** from the posts goes into `projects/linkedin-branding/engagement/problems.md` as a content idea.
- **No viral posts and no random CEOs.** Reach from the wrong audience does not count.
- Every comment adds a real point in his voice. No "Great post", no agreeing only. Skip politics, religion, tragedy and engagement bait.

## Never use
- Emojis
- Dashes of any kind (em dash, en dash, or a hyphen used as a dash)
- Cliché lines ("In today's fast-paced world", "Game changer", "Let that sink in", "Here's the thing", "I'm thrilled to announce")
- Long rows of hashtags. Use 3 at most, and only when useful.

## Originality
- No plagiarism. Trends and other people's posts are for inspiration only. Never copy their lines or structure.
- When someone else's data or idea is used, credit them.

## Facts
- Use only real facts from `projects/linkedin-branding/project-facts.md` or from Faizan himself. Never invent numbers, dates, times or stories.
- Do not name companies (employers, recruiters, clients) in a post without Faizan's OK.
- **Never use the client acquisition system as an example** in posts, comments or replies: it has never been run. Use the job search agent (running daily) or the Paperclip AI team for LinkedIn instead.

## Output format (paste-ready)
- Every final post gets two files in `projects/linkedin-branding/drafts/`:
  - `post-NN-short-name.md`: the post, plus the trend note and checks for Faizan
  - `post-NN-short-name.txt`: **only the post text** (no markdown, no headings, no notes), with a blank line between paragraphs
- Faizan opens the .txt in Notepad, presses Ctrl+A and Ctrl+C, then pastes it into LinkedIn. Copying from the .md file or from chat loses the line breaks.
- Once a post is published, mark the .md status as "POSTED on LinkedIn, YYYY-MM-DD".

## After posting
- Remind Faizan that the first 1 to 2 hours matter most: reply to comments quickly. He can paste the comments in to get ready-made replies.

## Trends
- Before drafting, check what is currently trending in AI automation, Claude and AI agents, and tie the post to it where it fits naturally.
- With each draft, add a short note for Faizan (not part of the post): which trend it uses and what he should learn from it.

## Images
- **Every post gets its own image, made with the post.** Never hand over a post without one.
- **Style: pencil sketch.** Graphite on off white paper, like H, HB and 2B pencil shading: 2B for headings and outlines, HB for body text, H for light hatching and notes. Hand drawn lines, hatching instead of colour fills. No colour, no photos, no stock icons.
- **Format: carousel.** 4 to 7 slides that walk through the post (cover with the hook, one idea per slide, last slide with the question, a boxed "Open to full time, part time and freelance work in AI automation, AI operations and business process automation. Have a boring, repetitive task to automate? Get in touch." and his name; template: post 04 slide 5). LinkedIn takes a carousel as a PDF document upload. Upload the PDF with "+" then **Add a document**, never the PNGs with the photo icon: photos show as a grid and LinkedIn crops the left side of the cover (happened with post 3 on 2026-10-21). Remind Faizan of this every time.
- Every slide is 1080 x 1080 square, with the content filling the whole frame. No border line or frame inside the slide: in the LinkedIn document viewer it looks like an empty band around the slide. Portrait or landscape images show black side bars in some LinkedIn views.
- Same writing rules on the slides: no emojis, no dashes, only real facts.
- How to build it: an HTML file with SVG pencil filters (template: `projects/linkedin-branding/drafts/post-03-paperclip-ai-team-carousel.html`), rendered with headless Edge into `slide-N.png` files, then one light PDF made from the PNGs (printing the HTML straight to PDF gives about 90 MB). Check every slide by eye for overlapping text before handing over.
- Files next to the post: `post-NN-short-name-carousel.html`, `post-NN-carousel/slide-N.png`, `post-NN-short-name-carousel.pdf`.
