# Finding and reading an app

This file deliberately names no individual app. Apps are added over time; find out the current ones and
each app's details from the sources below instead of from a fixed list.

## Which apps exist

In this order, use the first that works:

1. The portal page https://yukmmz.github.io/ — every published app has a card with its name, a short
   description and a link to `https://yukmmz.github.io/<app>/`.
2. `gh repo list yukmmz --visibility public --no-archived` (needs `gh`).
3. https://github.com/yukmmz?tab=repositories in the browser.

The repository of an app is `https://github.com/yukmmz/<app>`, where `<app>` is the last part of its URL.
Skip repositories that are not apps (for example `yukmmz.github.io` itself, or this kit).
Show the user a short list (name + one line) and let them choose.

## What kind of app it is

Decide from the files at the top of the repository:

| Files present | Kind | Run locally | Publish |
|---|---|---|---|
| `index.html`, no `package.json` | Static HTML/JS (most apps) | `python3 -m http.server 8000`, open http://localhost:8000/ | GitHub Pages from `main` / `/ (root)` |
| `package.json` with a `build` script (e.g. Vite) | Needs a build | `npm install`, then the `dev` script | Whatever `package.json` says: a `deploy` script (e.g. `gh-pages -d dist` → Pages from the `gh-pages` branch), or a GitHub Actions workflow in `.github/workflows/` |
| `pyproject.toml` / `*.py`, no `index.html` | Desktop program (Python) | the command in the README (typically `uv run python <file>.py`) | No web page; publishing = pushing the repository so others can download it |

## How to run and test it

Each app's `README.md` / `README_ja.md` has a development section (search for `http.server`, `npm`,
`uv run`, or `test`) with the exact commands. Also check `package.json` → `scripts`. Prefer what the
README says over the table above.

Tests usually live in `tests/` and run with Node.js (`node tests/<file>.js` or `node --test`); Node is
optional — skip the tests if it is not installed and the user does not want to install it. Shell loops
such as `for t in ...; do ...; done` do not work in Windows PowerShell; run each file separately there.

## Author-specific spots to replace (SKILL.md step 5)

Search the whole project (excluding `node_modules/` and `dist/`):

```
grep -rn --exclude-dir=node_modules --exclude-dir=dist -e "yukmmz" -e "script.google.com" -e "FEEDBACK_URL" .
```

What you will typically find, and what to do:

| Found | Meaning | Action |
|---|---|---|
| `FEEDBACK_URL` = `https://script.google.com/...` | The FB button sends to the original author | Remove the FB button/window, or use the user's own endpoint |
| `APP_URL`, `SRC_URL`, `PORTAL_URL` | Share/QR/"Other apps" targets | Point to the user's own addresses, or remove |
| `<meta property="og:url">`, `og:image` in `index.html` | Link previews | User's own address (must be absolute) |
| `https://yukmmz.github.io/` link ("Other apps") | Original author's portal | Remove or label as the original author's apps (ask) |
| `qr.svg`, `src-qr.svg` | QR codes to the original app/source | Delete with the code that shows them, or regenerate |
| `homepage` in `package.json`, `base` in `vite.config.*` | Build output paths | `https://<user>.github.io/<repo>/` and `/<repo>/` — must match the repository name |
| `manifest.webmanifest` | Installable-app info | Update name/URLs if they point to the original |
| mentions inside code comments | History only | Leave them |

## Things that make changes appear (or not)

- **Version and changelog.** Apps with `APP_VERSION` and a `CHANGELOG` often have a test that checks they
  match. After a change, raise the version and add an entry (or reset both to the user's own history).
- **Offline cache.** If the repository has `sw.js` (a service worker), browsers keep the old files until
  its cache name/version changes. Bump it with each published change.
- **Translations.** Many apps switch Japanese/English. UI text is kept in a strings table (look for
  `STRINGS` or `strings.*` and `i18n.js`), not written directly into HTML. Add new text to both languages,
  or ask the user whether one language is enough for their copy.
