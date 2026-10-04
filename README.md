# App Remix Kit

*English / [日本語](README_ja.md)*

A kit for turning the small apps at [yukmmz.github.io](https://yukmmz.github.io/) into **your own version with the help of an AI agent, and publishing it at your own URL**.
It is meant for people who have never used programming, GitHub, or AI agents such as Claude Code or Codex.

The apps are simple. Feel free to copy them, change them with AI, and make them your own (MIT License).

## What's inside

- This guide
- A skill for the AI: `skills/remix-app/`
  - `SKILL.md` — the procedure the AI follows: get the code → change it → try it → publish, one step at a time with you.
  - `references/` — the app catalog, and how to create a GitHub account and publish.

With the skill installed, the AI already knows how to proceed. You say what you want, and only act when the AI asks you to click something or sign in.

## What you need

1. **A computer** (Mac / Windows / Linux)
2. **An AI agent** (any one)
   - **Claude Code** — for a first try, the "Code" tab of the Claude desktop app is the easiest. Requires a paid plan.
   - **Codex** (OpenAI)
   - Any other AI that can read and write files on your computer and run commands
3. **A GitHub account** — only if you want to publish. The AI will guide you through creating one. Not needed for using the app on your own computer.

You don't need Git or other tools installed beforehand; the AI checks and helps you install what is missing.

## Getting started

### 1. Download this kit

Press **Code** → **Download ZIP** at the top of this page and unzip it (or `git clone https://github.com/yukmmz/app-remix-kit.git`).

### 2. Install the skill

Copy the `skills/remix-app` folder to:

| AI | Destination |
|---|---|
| Claude Code | `~/.claude/skills/remix-app/` (`~` is your home folder) |
| Codex | `~/.codex/skills/remix-app/` |

If you're not sure how, ask the AI in step 3:

> Install skills/remix-app from this folder (where I unzipped it) as a skill you can use.

For an AI without skills, start each session with:

> Read skills/remix-app/SKILL.md and follow it to help me.

### 3. Ask the AI

Open the AI in a working folder (for example a new `my-apps` folder on your desktop) and say what you want in plain words. For example (replace the app and the change with your own):

> (Example) Use the remix-app skill. I want my own version of multitask-timer where I can pick any color for each task.

In Claude Code you can also type `/remix-app`.

### 4. Work through it together

The AI asks what to change and whether to publish, gets the code (fork or ZIP), runs the original once, agrees the changes with you, replaces the original author's links and feedback address with yours, makes the changes in small steps for you to try, saves them, and — if you want — publishes them on GitHub Pages at `https://<your-username>.github.io/<app>/`.

## Apps

See the portal at https://yukmmz.github.io/ (source code: https://github.com/yukmmz?tab=repositories). The kit keeps working as new apps are added: the AI looks up the current ones.

## Good to know

- **What you publish is public.** Don't put passwords or personal data into the app. The skill tells the AI to ask you before anything is published.
- **The original apps stay unchanged.** You only change your own copy, and you can always start over from the original.
- **License (MIT).** You may change, publish and share freely; keep the original copyright line in `LICENSE`.
- AI usage costs follow your AI service's plan.

## Feedback

Please send comments, bug reports and requests about this kit with the **FB** button at the top right of the portal https://yukmmz.github.io/.
(About this kit or the original apps — not about your own remixed version.)

## License

This kit is also [MIT licensed](LICENSE).
