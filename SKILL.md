---
name: omarchy
description: "Manage and configure Omarchy Linux systems: edit Hyprland window manager settings, switch themes, customize keybindings, adjust monitors, manage waybar, and run omarchy-* CLI commands. Use when user asks about Omarchy, Hyprland, themes, keybindings, system config, or any omarchy-* commands."
---

# Omarchy Skill

Manage [Omarchy](https://omarchy.org/) Linux systems using natural language.

## ⛔ NEVER MODIFY CORE FILES

**DO NOT edit, write, or delete any files in `~/.local/share/omarchy/`**

This directory contains Omarchy's core system files. User configuration belongs in `~/.config/` instead.

If you need to change behavior controlled by a file in `~/.local/share/omarchy/`, find or create the corresponding override in `~/.config/`.

## Discovery

Omarchy provides ~145 commands following the pattern `omarchy-<category>-<action>`.

### Find Commands

```bash
# List all omarchy commands
compgen -c | grep -E '^omarchy-' | sort -u

# Find commands by category
compgen -c | grep -E '^omarchy-theme'
compgen -c | grep -E '^omarchy-restart'

# Read a command's source to understand it
cat $(which omarchy-theme-set)
```

### Command Categories

| Prefix | Purpose | Example |
|--------|---------|---------|
| `omarchy-refresh-*` | Reset config to Omarchy defaults (backs up first) | `omarchy-refresh-waybar` |
| `omarchy-restart-*` | Restart a service/app | `omarchy-restart-waybar` |
| `omarchy-toggle-*` | Toggle feature on/off | `omarchy-toggle-nightlight` |
| `omarchy-theme-*` | Theme management | `omarchy-theme-set <name>` |
| `omarchy-install-*` | Install optional software | `omarchy-install-docker-dbs` |
| `omarchy-launch-*` | Launch apps | `omarchy-launch-browser` |
| `omarchy-cmd-*` | System commands | `omarchy-cmd-screenshot` |
| `omarchy-pkg-*` | Package management | `omarchy-pkg-install <pkg>` |
| `omarchy-setup-*` | Initial setup tasks | `omarchy-setup-fingerprint` |
| `omarchy-update-*` | System updates | `omarchy-update` |

## Configuration Locations

### Hyprland (Window Manager)

```
~/.config/hypr/
├── hyprland.conf      # Main config (sources others)
├── bindings.conf      # Keybindings
├── monitors.conf      # Display configuration
├── input.conf         # Keyboard/mouse settings
├── looknfeel.conf     # Appearance (gaps, borders, animations)
├── envs.conf          # Environment variables
├── autostart.conf     # Startup applications
├── hypridle.conf      # Idle behavior (screen off, lock, suspend)
├── hyprlock.conf      # Lock screen appearance
└── hyprsunset.conf    # Night light / blue light filter
```

**Restart/Refresh:**
- `omarchy-refresh-hyprland` - Reset to defaults
- Hyprland auto-reloads on config save (no restart needed)
- `omarchy-restart-hypridle` / `omarchy-restart-hyprsunset` for those services

### Waybar (Status Bar)

```
~/.config/waybar/
├── config.jsonc       # Bar layout and modules (JSONC format)
└── style.css          # Styling
```

**Restart/Refresh:**
- `omarchy-restart-waybar` - Restart waybar
- `omarchy-refresh-waybar` - Reset to defaults
- `omarchy-toggle-waybar` - Show/hide

### Walker (App Launcher)

```
~/.config/walker/
└── config.toml        # Launcher configuration
```

**Restart/Refresh:**
- `omarchy-restart-walker`
- `omarchy-refresh-walker`

### Terminals

```
~/.config/alacritty/alacritty.toml
~/.config/kitty/kitty.conf
~/.config/ghostty/config
```

**Restart:**
- `omarchy-restart-terminal`

### Other Configs

| App | Location |
|-----|----------|
| btop | `~/.config/btop/btop.conf` |
| fastfetch | `~/.config/fastfetch/config.jsonc` |
| lazygit | `~/.config/lazygit/config.yml` |
| starship | `~/.config/starship.toml` |
| git | `~/.config/git/config` |

## Safe Editing Pattern

When modifying any Omarchy config:

### 1. Read Current Config

```bash
cat ~/.config/<app>/config
```

### 2. Backup Before Changes

```bash
cp ~/.config/<app>/config ~/.config/<app>/config.bak.$(date +%s)
```

### 3. Make Changes

Use the Edit tool. Preserve existing structure and comments.

### 4. Apply Changes

```bash
# For most apps, use the restart command
omarchy-restart-<app>

# Or reset to defaults (creates backup automatically)
omarchy-refresh-<app>
```

### 5. Explain What You Did

After completing changes, include a brief **Learn More** block explaining what files were modified, why, and key config options that were set.

## Common Tasks

### Themes

```bash
omarchy-theme-list              # Show available themes
omarchy-theme-current           # Show current theme
omarchy-theme-set <name>        # Apply theme
omarchy-theme-next              # Cycle to next theme
omarchy-theme-bg-next           # Cycle wallpaper
omarchy-theme-install <url>     # Install from git repo
```

### Keybindings

Edit `~/.config/hypr/bindings.conf`. Format:
```
bind = SUPER, Return, exec, xdg-terminal-exec
bind = SUPER, Q, killactive
bind = SUPER SHIFT, E, exit
```

View current bindings: `omarchy-menu-keybindings`

### Display/Monitors

Edit `~/.config/hypr/monitors.conf`. Format:
```
monitor = eDP-1, 1920x1080@60, 0x0, 1
monitor = HDMI-A-1, 2560x1440@144, 1920x0, 1
```

List monitors: `hyprctl monitors`

### Screenshots

- `omarchy-cmd-screenshot` - Interactive screenshot
- `omarchy-cmd-screenrecord` - Toggle screen recording

### System

```bash
omarchy-update                  # Full system update
omarchy-version                 # Show Omarchy version
omarchy-debug                   # Debug info for troubleshooting
omarchy-lock-screen             # Lock screen
omarchy-cmd-shutdown            # Shutdown
omarchy-cmd-reboot              # Reboot
```

## Fonts

```bash
omarchy-font-list               # Available fonts
omarchy-font-current            # Current font
omarchy-font-set <name>         # Change font
```

## Troubleshooting

```bash
# Check Omarchy state
omarchy-state

# Debug information
omarchy-debug

# Upload logs for support
omarchy-upload-log

# Reset specific config to defaults
omarchy-refresh-<app>

# Full reinstall (nuclear option)
omarchy-reinstall
```

## Omarchy Manual

**IMPORTANT:** For general "how do I" questions, ALWAYS fetch the relevant manual page BEFORE answering. The manual at `https://learn.omacom.io` contains Omarchy-specific guidance that may differ from generic Linux advice.

### When to Fetch the Manual

**Always fetch first** when users ask:
- "How do I..." / "What is..." / "Why does..." questions
- Questions about installing/running software (Windows, games, apps)
- Questions about concepts, workflows, or best practices
- Topics where Omarchy may have a specific approach

### Manual Index

See [MANUAL_INDEX.md](MANUAL_INDEX.md) for the full topic-to-URL lookup table (35+ topics with keywords).

### Fetching Manual Pages

When a user asks a general question:

1. **Identify relevant topic(s)** from [MANUAL_INDEX.md](MANUAL_INDEX.md)
2. **Fetch the page** using WebFetch with full URL: `https://learn.omacom.io<path>`
3. **Extract and summarize** the relevant information for the user

**Examples:**
- "How do I set up my fingerprint reader?" → Fetch `/2/the-omarchy-manual/77/fingerprint-fido2-authentication`
- "How do I install Windows on Omarchy?" → Fetch `/2/the-omarchy-manual/100/windows-vm`
- "How do I install Steam?" → Fetch `/2/the-omarchy-manual/71/gaming`

