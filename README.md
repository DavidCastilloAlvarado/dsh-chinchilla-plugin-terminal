# dsh-chinchilla-plugin-terminal

Bottom terminal panel for the DeepSeek Harness (DSH) Web GUI — a multi-tab shell pinned to the bottom of the page (openpty on Linux/macOS, ConPTY on Windows).

MIT

## Install

```sh
dsh plugin --profile web add dsh-chinchilla-plugin-terminal && dsh web
```

Toggle with **Ctrl+\`** (configurable). This is a DSH plugin — install it with `dsh plugin`, not plain `npm i`.

Uninstall:

```sh
dsh plugin --profile web remove dsh-chinchilla-plugin-terminal
```

| Collapsed | Expanded | Multi-tab |
|---|---|---|
| ![collapsed](docs/screenshot-collapsed.png) | ![panel](docs/screenshot-panel.png) | ![multitab](docs/screenshot-multitab.png) |

## Features

- Multi-tab: `+` new, ✕ close, ⟳ restart; processes keep running on tab switch
- New terminals open in the workspace of the conversation they were opened in; ⟳ restart inherits the tab's directory; hover a tab to see its working directory
- Terminals survive `dsh web` restarts: sessions and scrollback are persisted under `$DSH_HOME/plugin-data/terminal/` and come back as "exited" history tabs
- xterm.js 6, 10000-line scrollback, drag-to-resize panel, configurable toggle shortcut

## Configuration

Settings live in `$DSH_HOME/settings.yaml` (section `terminal`), editable under **Settings → Plugins**. Changes apply to new tabs — no restart needed.

| Field | Default | Meaning |
|---|---|---|
| `toggleShortcut` | `ctrl+`` | Panel toggle shortcut, e.g. `ctrl+j`, `ctrl+shift+f1` |
| `shellCommand` | *(empty — auto-detect)* | Command line for **new** sessions; empty = platform default (`$SHELL` / pwsh) |

## Local development

```sh
git clone https://github.com/DavidCastilloAlvarado/dsh-chinchilla-plugin-terminal.git
cd dsh-chinchilla-plugin-terminal
npm install        # also runs npm run build
dsh plugin --profile web add /absolute/path/to/dsh-chinchilla-plugin-terminal
dsh web
```

- Changed `src/` (client) → `npm run build`, restart `dsh web`, hard-refresh the browser
- Changed `lib/index.js` (server) → restart `dsh web`
- `npm test` runs the full suite
- It's a link install: the plugin resolves deps from the checkout's `node_modules` — don't move or delete the checkout while the profile uses it
