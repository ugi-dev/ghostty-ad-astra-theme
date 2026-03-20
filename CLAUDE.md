# Ghostty Ad Astra — notes for Claude Code

This repository ships **two** Ghostty theme files (no extension): `ad-astra-dark` and `ad-astra-light`. They belong in `~/.config/ghostty/themes/`; the user’s Ghostty config then sets `theme = ad-astra-dark` / `ad-astra-light` or the combined light/dark line.

## Skill

The install workflow lives in **`.claude/skills/ad-astra-ghostty/SKILL.md`**.

- **Slash command:** `/ad-astra-ghostty` (optional args: `dark`, `light`, or `system`)
- **Auto:** Claude can load the same skill when the user asks to install or apply this theme on Ghostty.

That skill uses **`${CLAUDE_SKILL_DIR}`** to find the repo root (theme files sit three levels above the skill directory).

## References

- Human-readable setup: [README.md](README.md)
- Ghostty: [themes](https://ghostty.org/docs/features/theme), [config paths](https://ghostty.org/docs/config)
