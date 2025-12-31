# Omarchy Skill

An agent skill for managing [Omarchy](https://omarchy.org/) Linux systems using natural language.

## Overview

This skill enables AI coding agents to configure and manage Omarchy systems. It uses a discovery-based approach - teaching the agent how to find and understand Omarchy's ~145 commands rather than hardcoding documentation that goes stale.

## Installation

### Claude Code

```bash
git clone https://github.com/robzolkos/omarchy-skill.git ~/.claude/skills/omarchy
```

### OpenCode

```bash
git clone https://github.com/robzolkos/omarchy-skill.git ~/.config/opencode/skill/omarchy
```

## Usage

Once installed, your agent will automatically use this skill when you ask about Omarchy. Examples:

- "Change my theme to catppuccin"
- "Add a keybinding for Super+E to open file manager"
- "Configure my external monitor"
- "Make the window gaps smaller"
- "Set up night light to turn on at sunset"
- "Show me what omarchy commands are available for bluetooth"
- "Increase waybar height"
- "Change my terminal font"

## What's Covered

- **Hyprland** - Window manager, keybindings, monitors, appearance
- **Waybar** - Status bar modules and styling
- **Walker** - App launcher
- **Themes** - System-wide theming
- **Terminals** - Alacritty, Kitty, Ghostty
- **System** - Updates, screenshots, screen recording, power

## Discovery-Based Approach

Instead of exhaustively documenting every command, this skill teaches agents to discover commands dynamically:

```bash
# Find all omarchy commands
compgen -c | grep -E '^omarchy-' | sort -u

# Read a command's source
cat $(which omarchy-theme-set)
```

This means the skill stays current as Omarchy evolves.

## Requirements

- [Omarchy](https://omarchy.org/)

## Related

- [omarchy-waybar-skill](https://github.com/robzolkos/omarchy-waybar-skill) - Focused skill for Waybar configuration

## License

MIT
