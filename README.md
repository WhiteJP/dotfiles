# Dotfiles

Personal defaults for Git, Cursor, VS Code, and RStudio. Clone this repository anywhere on disk, then run **one script** to configure Git globally and symlink editor and RStudio settings.

## Quick start

1. Clone this repository (any path you like).
2. From a terminal in the clone, run:

   ```bash
   ./script/bootstrap
   ```

   Use **bash** (macOS Terminal, Linux, WSL, or **Git Bash** on Windows).

That will:

- Set **global Git** options (ignore file, attributes, line endings, `filemode`) using [`script/bootstrap-git`](script/bootstrap-git).
- **Symlink** [`editor/settings.json`](editor/settings.json) into Cursor and VS Code user config dirs, and [`rstudio/rstudio-prefs.json`](rstudio/rstudio-prefs.json) into RStudio’s prefs path for your OS.

If a target file already exists and is not already a link to this repo, it is **renamed** to `*.bak.<timestamp>` next to the original name so nothing is lost silently.

**Windows:** Symlinks from Git Bash need a normal user account that may create them (Windows **Developer Mode** on, or an elevated shell, depending on your policy). If `ln -sf` fails, enable Developer Mode under Settings → Privacy & security → For developers, then run `./script/bootstrap` again.

Git-only (no app symlinks): `./script/bootstrap-git`

## What gets configured (Git)

| Setting | macOS / Linux / WSL | Windows (Git Bash / Git for Windows) |
|--------|----------------------|--------------------------------------|
| `core.excludesfile` | This repo’s `git/gitignore_global` | Same |
| `core.attributesfile` | `git/gitattributes_global.unix` | `git/gitattributes_global.windows` |
| `core.autocrlf` | `input` | `true` |
| `core.eol` | `lf` | `crlf` |
| `core.filemode` | `true` | `false` |

**WSL** reports as Linux, so it uses the **Unix** profile (not the Windows Git profile).

### Global ignore patterns

[`git/gitignore_global`](git/gitignore_global) ignores, among other things, `.vscode/`, `.cursor/`, `.history/`, and `.claude/` in **every** repository on this machine. To track any of those in a specific project, override in that repo’s `.gitignore` (for example `!.claude/` where appropriate) or use `git add -f` only when you intend to commit them.

## Cursor and VS Code settings

Canonical copy: [`editor/settings.json`](editor/settings.json) (final newline, trim trailing whitespace, format on save, word wrap, diff editor colors). `bootstrap` links it to:

| OS | Cursor | VS Code |
|----|--------|---------|
| macOS | `~/Library/Application Support/Cursor/User/settings.json` | `~/Library/Application Support/Code/User/settings.json` |
| Linux / WSL | `$XDG_CONFIG_HOME/Cursor/User/settings.json` (default `~/.config/...`) | same under `Code/User/` |
| Windows | `%APPDATA%\Cursor\User\settings.json` | `%APPDATA%\Code\User\settings.json` |

`editor.formatOnSave` only helps where a formatter is installed for that language.

## RStudio preferences

Canonical copy: [`rstudio/rstudio-prefs.json`](rstudio/rstudio-prefs.json). Linked to:

| OS | Path |
|----|------|
| macOS | `~/Library/Application Support/RStudio/rstudio-prefs.json` |
| Linux / WSL | `~/.config/rstudio/rstudio-prefs.json` |
| Windows | `%APPDATA%\RStudio\rstudio-prefs.json` |

If the editor theme does not apply, open **Tools → Global Options → Appearance** and pick **Pastel on Dark** once; if the internal name differs, update the `editor_theme` value in this repo to match.

## Repository layout

| Path | Purpose |
|------|---------|
| `git/gitignore_global` | Global excludes (referenced by Git) |
| `git/gitattributes_global.unix` / `git/gitattributes_global.windows` | Global attributes (per OS) |
| `script/bootstrap` | **Recommended:** Git + app symlinks |
| `script/bootstrap-git` | Git global configuration only |
| `script/link-app-settings` | Cursor / VS Code / RStudio symlinks only |
| `editor/settings.json` | Cursor / VS Code user settings |
| `rstudio/rstudio-prefs.json` | RStudio user preferences |
