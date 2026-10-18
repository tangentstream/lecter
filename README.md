# tangentstream/lecter


Lecter = Decker + Electron. 

Wraps the JavaScript/web build of [Decker](https://github.com/JohnEarnest/Decker) — a
hypercard-like multimedia authoring tool — as a desktop Electron app, in order
to give web-Decker **local file access** (file read/write + shell commands) via
an IPC bridge into the Decker "danger zone".

**Stream:**

[![decker + electron = ???](https://img.youtube.com/vi/d_uvx_iQ7kk/0.jpg)](https://www.youtube.com/watch?v=d_uvx_iQ7kk)

"decker + electron = ???" (tangentstream, 2025-10-16) — attempting to add local
file access to web-decker through electron.

## Build / run

```sh
npm install
npm start      # electron .
```

`package.json`: package `lecter` 1.0.0, `electron` ^28.0.0 as a devDependency.
The window loads `lecter-deck.html` and injects the toolbar/color/danger-zone
setup automatically.

## Repo layout

- `index.js` — Electron main process
- `preload.js` — IPC bridge (file + shell) exposed to the page
- `lecter-deck.html` — bundled Decker deck
- `decker/` — vendored Decker source
- `todo.md`, `GEMINI.md` — task list + agent notes on Decker internals
- `package.json`, `.gitignore`, `README.md` (two lines), `LICENSE.txt`
