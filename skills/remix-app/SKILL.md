---
name: remix-app
description: Guide a beginner (new to programming, GitHub and AI agents) through making their own version of one of yukmmz's small web apps (yukmmz.github.io) — get the code (fork, clone or ZIP), change it the way they want, run it, and publish it on their own GitHub Pages. Use when the user says things like "I want to customize this app", "make my own version of <app>", "add a feature to <app> for myself", "remix", or "publish my version on GitHub".
---

# Remix one of yukmmz's apps into your own

The apps at https://yukmmz.github.io/ are small, dependency-free tools released under the MIT License.
Their author **wants** people to copy them and change them freely with AI. Your job is to take a person
who may never have used a terminal, Git or GitHub from "I'd like this app to do X" to "my own version is
running at my own URL", one small step at a time.

How to find the current apps, tell what kind each one is, run and test it, and locate the
author-specific spots is in [references/app-anatomy.md](references/app-anatomy.md). This kit keeps no
fixed list of apps: always look them up there. The GitHub account and publishing steps are in
[references/publish-to-github.md](references/publish-to-github.md). Read them when you reach those steps.

## How to talk to the user

- Reply in the user's language.
- Assume no background. When a term first appears (repository, fork, commit, push, terminal, GitHub Pages),
  explain it in one plain sentence. Do not lecture beyond that.
- **One step at a time.** Give one action, wait for the result, then the next. Never paste a 15-step list
  and leave the person alone with it.
- Do the work yourself whenever you can (edit files, run commands). Only ask the user to act when it needs
  their hands: creating an account, clicking in a browser, typing a password, approving a prompt.
- When something fails, read the actual error, explain it in one sentence, and fix it. Do not guess.

## Safety rules (always)

- Ask before anything that goes **outside the user's computer**: pushing, creating a repository, making
  it public, enabling GitHub Pages. Say plainly that the result will be visible to anyone on the internet.
- Never push to, open pull requests against, or otherwise write to the **original author's repository**
  (`github.com/yukmmz/...`) unless the user explicitly asks to send a contribution.
- Never put passwords, tokens, API keys or personal data into the code. A GitHub Pages site is public.
- Never delete the user's files or run destructive Git commands (`reset --hard`, `push --force`,
  `clean -fd`) without explaining what will be lost and getting a yes.
- Keep the original `LICENSE` file and its copyright line. The MIT License requires it. Add the user's
  own line below it (see step 5).

## Step 1. Find out where the user stands

Ask only what you cannot detect yourself. Detect the OS and installed tools by running commands
(`git --version`, `gh --version`, `node --version`, `python3 --version`, `uv --version`); do not ask the
user to check them. On Windows, check Python with `py --version` or `python --version` instead:
`python3` there is often only a shortcut that opens the Microsoft Store.

Ask, in one short message:

1. Which app do they want to start from? (If they don't know, look up the current apps as described in `references/app-anatomy.md` and show them.)
2. What do they want to change or add? A rough idea is enough; you will refine it in step 4.
3. Do they want to **publish** it on the internet (their own URL), or only use it on their own computer?
4. Do they already have a GitHub account?

## Step 2. Get the code

Pick **one** route from the answers and tell the user which and why, in one sentence.

| Situation | Route |
|---|---|
| Wants to publish, has a GitHub account (or is willing to make one now) | **A. Fork** (recommended) |
| Wants to publish, has an account, but does not want the "forked from" link | **B. New repository from a copy** |
| Only wants to use it locally, no account | **C. Download ZIP** |

If they want to publish but have no account, help them create one first
(`references/publish-to-github.md` § "Create a GitHub account"), then use route A.

### A. Fork

A fork is your own copy of the repository on GitHub that remembers where it came from.

- If `gh` is installed and logged in (`gh auth status`):
  `gh repo fork yukmmz/<app> --clone --remote` in the folder where the user keeps projects.
- Otherwise: have the user open `https://github.com/yukmmz/<app>`, press **Fork**, and **Create fork**.
  Then clone their fork: `git clone https://github.com/<their-name>/<app>.git`.
  If Git is not installed, see `references/publish-to-github.md` § "Install the tools".
- The user may rename the repository (GitHub → the fork → Settings → Repository name). If they do it,
  do it **now**, before step 5, because the public URL and some settings depend on the name.

### B. New repository from a copy

Clone the original (`git clone https://github.com/yukmmz/<app>.git <new-name>`), then remove the link to
the original: `git -C <new-name> remote remove origin`. The repository is created on GitHub in step 7.

### C. Download ZIP

Have the user open `https://github.com/yukmmz/<app>/archive/refs/heads/main.zip` (or the repository
page → **Code** → **Download ZIP**), unzip it, and tell you the folder path. Work in that folder.
If they later decide to publish, run `git init` there and follow route B from step 7.

After getting the code, confirm the folder exists and list its files.

## Step 3. Run the original once, unchanged

Before changing anything, start the app as it is and have the user open it, so both of you know the
starting point works. Find the app's kind and its start command as described in
`references/app-anatomy.md` (the app's README has the exact command). For the static HTML apps:

```
python3 -m http.server 8000
```

(on Windows: `py -m http.server 8000`, or `python -m http.server 8000`), then open http://localhost:8000/ in the browser. (Opening `index.html` by double-click often works too,
but some features such as the offline cache need the local server.) Stop the server with Ctrl+C when done.

## Step 4. Make it theirs: decide the changes

1. Read the app's `README.md` (or `README_ja.md`) and the main source files before proposing anything.
   The public repositories do not include the author's development notes, so the code is the reference.
2. Turn the user's wish into a short, concrete list (what they will see, what they will press, what
   happens). Ask about anything that changes the result; choose sensible defaults for the rest and say so.
3. If the wish is large, split it into small versions and start with the smallest one that is useful.
4. Show the list and get a "yes" before editing.

## Step 5. Replace the original author's personal parts

Do this **once, before or together with the first change**, so the user's copy never sends data to, or
links back as if it were, the original author's app.

- **Links and the feedback address.** Run the search in `references/app-anatomy.md` § "Author-specific
  spots" and handle each hit as its table says. The feedback button must never keep sending to the
  original author. URLs become the user's own `https://<their-name>.github.io/<repo-name>/` and
  `https://github.com/<their-name>/<repo-name>`; if they will not publish, remove share links instead.
- **Name and README.** Ask whether to rename the app. Rewrite the top of `README.md` / `README_ja.md`
  in the user's words, and add a line such as:
  "Based on [<original app>](https://github.com/yukmmz/<app>) by Yu Kamimizu (MIT License)."
- **LICENSE.** Keep the existing copyright line and add one below it:
  `Copyright (c) <year> <user's name>`.
- **Version and changelog.** Ask whether to reset them to the user's own history (for example `1.0.0`
  "First version of my copy") or keep adding entries; see `references/app-anatomy.md` § "Things that
  make changes appear".

Finally run the search again and show the user what remains.
Remaining mentions in code comments are harmless; anything the visitor can see or click should be handled.

## Step 6. Change, run, check — in small loops

For each item of the agreed list:

1. Edit the code. Follow the existing style and structure; keep the app dependency-free unless the user
   agrees to add something.
2. Run the app's tests if it has them (see the app's README and `references/app-anatomy.md`). If a test breaks because the behaviour
   changed on purpose, update the test and say so; otherwise fix the code.
3. Restart or reload the local app and ask the user to try exactly the thing that changed. Tell them what
   to press and what they should see.
4. Fix what they report, then move to the next item.

After a few working changes, offer to save a checkpoint (step 7's commit) so mistakes can be undone.

## Step 7. Save (commit)

A commit is a saved snapshot of the project that you can return to. It stays on the computer until pushed.

- First commit only: make sure Git knows who they are
  (`git config --global user.name` / `user.email`; for privacy suggest GitHub's
  `<id>+<name>@users.noreply.github.com` address shown at GitHub → Settings → Emails).
- Show the list of changed files, then commit with a short message describing the change.
- Do not commit secrets, large videos/images the user did not mean to publish, or `node_modules/`.

## Step 8. Publish on GitHub Pages

Only after the user confirms they want it public. Follow `references/publish-to-github.md`:

- Route A (fork): push, then turn on Pages.
- Route B / C: create the repository on GitHub, push, then turn on Pages.
- Apps that need a build, and desktop (Python) apps, publish differently; see the "kind" table in
  `references/app-anatomy.md`.

Then wait about a minute, open `https://<their-name>.github.io/<repo-name>/`, and check that the change is
there. If the old version appears, reload (Safari/iPad may need two reloads).

## Step 9. Finish

Tell the user, in three or four lines:

- their app's address, and their repository's address;
- how to change it again later: open this folder with the AI and say what to change; the AI edits,
  commits and pushes after they agree;
- that the original author's app is untouched and they can always start again from it.
