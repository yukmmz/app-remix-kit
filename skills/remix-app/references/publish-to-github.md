# GitHub: account, tools, and publishing

Explain each part only when the user reaches it. Ask before every step that sends something to GitHub.

## Create a GitHub account

The user does this in the browser; you guide them.

1. Open https://github.com/signup.
2. Enter an email address, a password, and a **username**. Point out that the username becomes part of
   their app's address: `https://<username>.github.io/<app>/`. Short, lowercase, no personal full name
   unless they want it.
3. Verify the email with the code GitHub sends.
4. The free plan is enough. Skip the questionnaire if offered.
5. Recommend turning on two-factor authentication later (Settings → Password and authentication).

Ask the user to tell you the username when done.

## Install the tools

Check first; install only what is missing. Ask before installing anything.

- **Git** — macOS: `xcode-select --install` (or `brew install git` if Homebrew exists).
  Windows: `winget install --id Git.Git -e`, or the installer from https://git-scm.com/download/win.
  Linux: the distribution's package manager.
- **GitHub CLI (`gh`)** — optional but makes the rest easier. macOS: `brew install gh`.
  Windows: `winget install --id GitHub.cli -e`. Then `gh auth login` (choose GitHub.com → HTTPS →
  "Login with a web browser"; the user copies the one-time code into the browser).
- **No terminal at all?** GitHub Desktop (https://desktop.github.com/) can clone, commit and push with
  buttons. Guide the user through its menus instead of commands if they prefer it.

Without `gh`, the first `git push` over HTTPS opens a browser sign-in (Git Credential Manager on
Windows/macOS). If it asks for a password in the terminal instead, a normal password will not work:
install `gh` and run `gh auth login`, then `gh auth setup-git`.

## Push the code

### Route A (fork)

The fork already exists on GitHub and `origin` points to it.

```
git push origin main
```

### Route B / C (new repository)

Ask the user for the repository name (default: the app name). With `gh`:

```
gh repo create <repo-name> --public --source . --remote origin --push
```

Without `gh`: have the user open https://github.com/new, enter the name, choose **Public**, leave
"Add a README" **unchecked**, press **Create repository**, then:

```
git remote add origin https://github.com/<username>/<repo-name>.git
git branch -M main
git push -u origin main
```

(Route C only: run `git init`, `git add -A`, `git commit -m "First version of my copy"` first.)

GitHub Pages on a free account requires a **public** repository.

## Turn on GitHub Pages

With `gh` (static apps; for an app that deploys to a `gh-pages` branch, use `gh-pages` instead of `main`):

```
gh api -X POST repos/<username>/<repo-name>/pages -f "source[branch]=main" -f "source[path]=/"
```

Or in the browser: the repository → **Settings** → **Pages** → Source: "Deploy from a branch" →
Branch: `main`, folder `/ (root)` → **Save**.

A fork may show "GitHub Pages is disabled" until the first push or until Pages is saved once; saving the
setting again fixes it.

After 1–2 minutes the site is at `https://<username>.github.io/<repo-name>/`. Progress is visible in the
repository's **Actions** tab ("pages build and deployment"). Check it opens, then also set the
repository's **About → Website** field to that address so visitors can find it.

## Later updates

Edit → test → commit → `git push`. Static apps republish automatically. For apps with a `deploy` script, also run
`npm run deploy`.

## Common problems

| Symptom | Cause and fix |
|---|---|
| 404 at the Pages address | Pages not turned on, wrong branch/folder, or still building — check Settings → Pages and the Actions tab |
| Page loads but is blank / styles missing (apps that need a build) | `base` in `vite.config.*` (or `homepage` in `package.json`) does not match the repository name |
| Old version still shows | Browser cache — reload; on iPad/Safari reload twice; if the app has `sw.js`, bump its cache name |
| `rejected ... fetch first` on push | GitHub has commits the computer does not (e.g. edited on the website) — `git pull --rebase`, then push |
| `Permission denied` / `403` | Pushing to someone else's repository (e.g. the original) or not logged in — check `git remote -v` and `gh auth status` |
