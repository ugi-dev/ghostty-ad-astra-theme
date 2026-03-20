---
name: ad-astra-ghostty
description: Installs the Ad Astra Ghostty color theme (dark/light) by copying theme files into Ghostty’s themes directory and setting `theme` in the user’s config. Use when the user wants Ad Astra on Ghostty, asks to install or apply this repo’s Ghostty theme, or mentions Ghostty theming together with Ad Astra.
argument-hint: "[dark|light|system]"
---

# Ad Astra for Ghostty

Help the user **install and enable** the theme from this repository: `ad-astra-dark` and `ad-astra-light` (no file extension). Official references: [Ghostty themes](https://ghostty.org/docs/features/theme), [config locations](https://ghostty.org/docs/config).

## Claude Code only

- **Invoke directly:** `/ad-astra-ghostty` — same as this skill’s `name` in frontmatter. Optional: `/ad-astra-ghostty dark`, `light`, or `system` (see [passing arguments](https://docs.anthropic.com/en/docs/claude-code/skills#pass-arguments-to-skills)).
- **Repo root with bundled themes:** when this project skill is active, `${CLAUDE_SKILL_DIR}` is the folder containing this `SKILL.md`. Compute the checkout root (where the theme files live):

```bash
REPO_ROOT="$(cd "${CLAUDE_SKILL_DIR}/../../.." && pwd)"
# Must contain ad-astra-dark and ad-astra-light
```

Use `REPO_ROOT` in `cp` commands instead of a hard-coded path when helping from a clone of `https://github.com/ugi-dev/ghostty-ad-astra-theme`.

- **User preference from arguments:** if `$ARGUMENTS` (or the first token after the slash command) is `dark`, `light`, or `system`, pick the matching `theme =` line below without asking again. If missing, ask once or default to **system** (light/dark pair).

## Before changing anything

1. Confirm **Ghostty is installed** (`ghostty --version` or equivalent). If missing, tell them to install Ghostty first; do not invent binaries.
2. Resolve **theme source path**: prefer `REPO_ROOT` from `${CLAUDE_SKILL_DIR}` as above; otherwise the directory containing `ad-astra-dark` and `ad-astra-light` (e.g. current workspace root if both files exist there).

## Install theme files

Ghostty loads custom themes from **`~/.config/ghostty/themes/`** by **filename** (no extension in the theme file names on disk).

Use this pattern (adjust source directory):

```bash
mkdir -p ~/.config/ghostty/themes
cp /path/to/ghostty-ad-astra-theme/ad-astra-dark /path/to/ghostty-ad-astra-theme/ad-astra-light ~/.config/ghostty/themes/
```

Verify:

```bash
test -f ~/.config/ghostty/themes/ad-astra-dark && test -f ~/.config/ghostty/themes/ad-astra-light && echo ok
```

**macOS note:** Some setups use `~/Library/Application Support/com.mitchellh.ghostty/` for config; theme directory rules are in Ghostty’s [config docs](https://ghostty.org/docs/config). Prefer the user’s actual layout if they already have a working `config` elsewhere.

## Enable in config

Locate the active **main** config file (common paths):

- `~/.config/ghostty/config`
- macOS: `~/Library/Application Support/com.mitchellh.ghostty/config`

Add **one** `theme =` line (later config files can override; see docs):

| Goal | Line |
|------|------|
| Dark | `theme = ad-astra-dark` |
| Light | `theme = ad-astra-light` |
| Match system | `theme = light:ad-astra-light,dark:ad-astra-dark` |

If a `theme =` line already exists, **replace** it or explain that the last wins across merged config files—avoid leaving conflicting duplicates without telling the user.

**Absolute path alternative** (no copy into `themes/`): `theme = /full/path/to/ad-astra-dark` (still no extension in the filename).

## Finish

Tell the user to **reload** Ghostty (**⌘⇧,** on macOS, **Ctrl⇧,** on Linux) or fully quit and reopen if the theme does not apply.

## Troubleshooting

- **Theme not found:** filenames must be exactly `ad-astra-dark` and `ad-astra-light`; check `ls ~/.config/ghostty/themes/`.
- **No visible change:** another `config-file` or `theme` override may apply—check `auto/theme.ghostty` if they use `+list-themes` workflow.
- **Permissions:** `~/.config/ghostty` must be writable.

## Do not

- Rename the theme files (breaks `theme = ad-astra-*` names).
- Strip or add a file extension to the theme files.
- Point users to unofficial downloads; prefer `https://github.com/ugi-dev/ghostty-ad-astra-theme` or their local clone.
