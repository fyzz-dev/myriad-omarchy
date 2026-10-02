# Myriad Omarchy

A [Myriad](https://github.com/fyzz-dev/myriad) addon that adds an "Omarchy" theme: it always matches your active
[Omarchy](https://omarchy.org) system theme (colours, borders and rounding), and switches whenever you run
`omarchy-theme-set`. On a fresh Myriad install on Omarchy it's the theme you start with. On systems without Omarchy it
does nothing.

## Install

Put `myriad-omarchy-<v>.jar` in `mods/` next to Myriad.

**Flatpak launchers** (like the Flatpak Prism Launcher) run the game in a sandbox that can't see your theme. The
Theme panel shows the fix when that happens; it's this, run once with the launcher closed:

```bash
flatpak override --user --filesystem=~/.local/state/omarchy:ro org.prismlauncher.PrismLauncher
```

## Build

1. In the Myriad repository, run `./gradlew publishToMavenLocal`.
2. Here, `./gradlew build` writes the jar to `build/libs/`. `./gradlew runClient` starts the game with Myriad,
   Myriad Essentials and this addon.
3. `./gradlew publishToMavenLocal` here too if you want the Myriad repo's dev client to load it.

## How it works

Omarchy keeps the active theme in `~/.local/state/omarchy/current/theme/`: a `colors.toml` with the terminal palette
and a `hyprland.lua`/`hyprland.conf` with border colours and rounding. The addon turns those into a Myriad
`ThemePalette`, registers the theme as `live` (Myriad re-applies it when the files change), and as an alias of the old
built-in id so choices and edits from before the split carry over.
