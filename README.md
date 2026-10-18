# Lecter — Decker + Electron

Lecter wraps the JavaScript version of [Decker](https://github.com/JohnEarnest/Decker)
(John Earnest's hypercard-like multimedia authoring tool) as a desktop
**Electron** app, in order to give web-Decker **local file access** from inside
a Decker deck.

📺 Built live on the tangentstream channel:
[**decker + electron = ???**](https://www.youtube.com/watch?v=d_uvx_iQ7kk)
(2025-10-16) — *"attempting to add local file access to web-decker through
electron."*

## How it works

- `index.js` (Electron main process) opens a 1920×1080 window, loads
  `lecter-deck.html`, and on `did-finish-load` injects setup scripts into the
  page: it enables the drawing toolbars and color mode
  (`toolbars_enable=1;dr.color=1;resize();`) and calls `endanger()` — Decker's
  "danger zone" switch that lets a deck run arbitrary JavaScript.
- `preload.js` bridges Node into the page via `contextBridge`, exposing four
  functions to any danger-zone deck as `window.ipcFoo()`:
  - `ipcDir(path)` — list a directory (`fs.readdirSync`)
  - `ipcRdTxt(path)` — read a UTF-8 text file (BOM-stripped)
  - `ipcWrTxt(path, text)` — write a UTF-8 text file
  - `ipcShell(cmd)` — run a shell command, returns `{e, o}` (exit code, output)
- `todo.md` tracks the next step: a `danger.js` module wrapping these calls for
  decks.

## Run it

```sh
npm install
npm start   # electron .
```

The window loads `lecter-deck.html` and applies the toolbar/color/danger-zone
setup automatically (DevTools open by default).

## Repo layout

| File | What |
|---|---|
| `index.js` | Electron main process |
| `preload.js` | IPC bridge: file + shell access for the page |
| `lecter-deck.html` | Bundled Decker deck (the "lecter logo" page) |
| `decker/` | Vendored copy of the [Decker](https://github.com/JohnEarnest/Decker) source |
| `todo.md` | Task list |
| `GEMINI.md` | Agent discovery notes on Decker's internals (immediate-mode GUI globals, Electron integration pattern) |
| `LICENSE.txt` | MIT-style — Decker © 2022–2025 John Earnest; Electron implementation © 2025 Michal Wallace |

## License

See [LICENSE.txt](LICENSE.txt): Decker Copyright © 2022–2025 John Earnest;
Electron Implementation © 2025 Michal Wallace.
