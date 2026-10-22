# Paperclip Basics (beginner notes)

_Source: third-party articles (Oct 2026). Check against the official docs at github.com/paperclipai/paperclip before relying on details._

## What it is
An open-source (MIT) platform that runs a team of AI agents as a "company". It is a Node.js server with a React dashboard that runs on your own machine.

## Key ideas
| Term | Meaning |
|---|---|
| Company | A group of agents working toward one goal |
| Org chart | Who reports to whom. A CEO agent sits at the top. |
| Goals | What the company is trying to achieve. Tasks link back to goals. |
| Heartbeat | A schedule that wakes an agent up to do work |
| Budget | A monthly spending cap per agent |
| Approvals / audit log | You approve important actions, and everything is logged |
| Adapter | The connector to the tool that actually does the work (Claude Code, Codex, Gemini CLI and others) |

## How it fits with Claude Code
Paperclip decides **when and why** an agent works. The Claude Code adapter decides **how**: it starts Claude Code with the task and context and collects the result. Paperclip is the manager and Claude Code is the worker.

## Things to verify during setup
- [ ] Install command and requirements
- [ ] How the Claude Code adapter authenticates (Pro subscription login or API key)
- [ ] How to set heartbeat frequency and budgets
