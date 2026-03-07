# Suganote Installer - Project Context

## Project Overview
Standalone Godot 4.5 app that installs and updates Suganote on Windows. Uses the `godot-installer` addon for all install/upgrade/rollback logic.

## Git Submodules

### godot-installer addon (`addons/godot-installer/`)
- **Source repo**: `github.com/graydwarf/godot-installer` (private)
- **This is a git submodule** — do NOT edit files in `addons/godot-installer/` directly in this repo
- **To make addon changes**: Clone/open the `godot-installer` repo, make changes there, push, then update the submodule here:
  ```bash
  git submodule update --remote addons/godot-installer
  git add addons/godot-installer
  git commit -m "chore: Update godot-installer submodule"
  ```
- **After cloning or pulling**: Run `git submodule update --init` to fetch submodule content

## Related Projects
- **`github.com/graydwarf/suganote`** — Main Suganote app (also uses godot-installer as submodule)
- **`github.com/graydwarf/godot-installer`** — Reusable installer addon (the shared dependency)

## Architecture
- `scenes/main.gd` — Shell that configures InstallerConfig for Suganote, parses CLI, wires UI
- `addons/godot-installer/` — All installer logic (submodule, do not edit here)
- `assets/` — Suganote branding (logo, icons)
- `license-config.json` — Supabase licensing keys (gitignored, create from template)

## Three Installer Modes
1. **First Install** (`--install`, default) — Shows location picker, fetches latest version, downloads and extracts
2. **Upgrade** (`--upgrade <manifest_path>`) — Reads pending-upgrade.json, downloads, verifies, backs up, extracts, launches, polls for success
3. **Rollback** (`--rollback <install_dir>`) — Restores .backup files in the given directory

## Configuration
- `license-config.json` — Required for version fetching. Copy from `license-config.template.json` and fill in Supabase licensing project publishable key and URL.
- InstallerConfig values are set in `main.gd` (app_name, exe_name, pck_name, accent_color)

## Technical Context
- **Platform**: Windows
- **Godot Version**: 4.5.stable
- **Godot Language**: GDScript
