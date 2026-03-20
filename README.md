# Ghostty Ad Astra Theme

Colors match the **Ad Astra** VS Code themes (cyan/teal + lavender). Official Ghostty help: [Color Theme](https://ghostty.org/docs/features/theme) · [Config file locations](https://ghostty.org/docs/config) · [All options](https://ghostty.org/docs/config/reference).

**Files:** `ad-astra-dark` and `ad-astra-light` (Ghostty theme snippets, no file extension).

---

## Agent skills (Claude Code & Cursor)

This repo includes an [Agent Skill](https://docs.anthropic.com/en/docs/claude-code/skills) so coding agents can install the theme for you:

- **Claude Code:** `.claude/skills/ad-astra-ghostty/SKILL.md` — also loaded as slash command **`/ad-astra-ghostty`** (try `/ad-astra-ghostty system` for light/dark by OS). Project notes for Claude live in [`CLAUDE.md`](CLAUDE.md).
- **Cursor:** `.cursor/skills/ad-astra-ghostty/SKILL.md`

After you clone the repo, enable project skills in your agent settings if needed, then ask something like: *Install the Ad Astra Ghostty theme from this repo (dark / light / match system).*

---

## Setup

### 1. Get the theme files

```bash
git clone https://github.com/ugi-dev/ghostty-ad-astra-theme.git
cd ghostty-ad-astra-theme
```

### 2. Install into Ghostty’s `themes` folder

Ghostty looks up custom themes by **filename** under `~/.config/ghostty/themes/` (see [docs](https://ghostty.org/docs/config) for XDG / macOS Application Support layouts).

```bash
mkdir -p ~/.config/ghostty/themes
cp ad-astra-dark ad-astra-light ~/.config/ghostty/themes/
```

Check:

```bash
ls ~/.config/ghostty/themes/ad-astra-dark ~/.config/ghostty/themes/ad-astra-light
```

### 3. Turn the theme on in your Ghostty config

Edit your real config file. Common paths:

- `~/.config/ghostty/config`
- macOS: `~/Library/Application Support/com.mitchellh.ghostty/config`

Ghostty can load **more than one** file; [later files override earlier ones](https://ghostty.org/docs/config) for the same setting.

Add **one** of the following blocks.

**Dark only**

```text
theme = ad-astra-dark
```

**Light only**

```text
theme = ad-astra-light
```

**Match system light / dark**

```text
theme = light:ad-astra-light,dark:ad-astra-dark
```

**No `themes/` copy — absolute path** (change to your machine’s path):

```text
theme = /path/to/ghostty-ad-astra-theme/ad-astra-dark
```

### 4. Reload Ghostty

Save the config, then reload: **⌘⇧,** (macOS) or **Ctrl⇧,** (Linux). If nothing changes, fully quit and reopen Ghostty.

---

## Optional: `+list-themes` and auto-saved theme

```bash
ghostty +list-themes
```

Pick **Ad Astra**, press **w** to write `auto/theme.ghostty`. Then you can add to your main config:

```text
config-file = ?auto/theme.ghostty
```

`?` = file may be missing at first. If `auto/theme.ghostty` sets `theme = …`, it can **override** another `theme =` line—delete or edit that auto file if the wrong theme appears.

Example (dark default + optional override file):

```text
theme = ad-astra-dark
config-file = ?auto/theme.ghostty
```

---

## VS Code

The [Ad Astra](https://marketplace.visualstudio.com/items?itemName=ugi-dev.ad-astra) extension and [source repo](https://github.com/ugi-dev/ad-astra) are the reference for these colors.

---

## Ship as a built-in Ghostty theme

Upstream themes come from [iterm2-color-schemes](https://ghostty.org/docs/features/theme); contribute there if you want Ad Astra bundled with Ghostty.
