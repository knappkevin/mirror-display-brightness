# Mirror Display Brightness

An enhanced display panel for the [Omarchy](https://omarchy.org) bar with
**per-monitor brightness targeting**. The stock display panel can only drive
the focused monitor — which is a problem when your external screen mirrors
the laptop panel, since a mirrored output can never take focus in Hyprland.

This plugin adds a target selector to the brightness section so you choose
which display the slider drives: the internal backlight, an external monitor
over DDC/CI, or either side of a mirrored pair.

## Features

- **Brightness target pills** — pick `eDP-1`, `HDMI-A-1`, or any connected
  output; the slider reads and writes that display only.
- **Mirror-friendly** — adjust the external monitor's brightness while it
  mirrors the laptop screen (impossible via focus on Hyprland 0.56+).
- **Per-display state** — slider always shows the *target's* current value,
  not the focused monitor's.
- **Working display enable/disable** — compatible with Hyprland 0.56's Lua
  parser (`hyprctl eval 'hl.monitor({...})'`), replacing the removed
  `hyprctl keyword` path.
- Full keyboard navigation (`j/k` sections, `h/l` pills, `Enter` activates,
  `Esc` closes) matching Omarchy panel conventions.
- Everything else from stock: text size, scale presets, wheel-on-icon
  brightness, OSD, shell IPC.

## Install

```sh
omarchy plugin add https://github.com/knappkevin/mirror-display-brightness.git --enable
```

## Usage

Open the panel from the bar display icon:

- **BRIGHTNESS · `<monitor>`** — the header names the current target.
- Click a pill under the slider (or `j/k` onto the row, then `h/l`) to
  retarget; drag as usual.
- DISPLAYS rows toggle outputs on/off — click works again on Hyprland 0.56+.

## Requirements

- Omarchy (Quattro shell) with Quickshell
- For external monitors: DDC/CI enabled on the display
  (`ddcutil detect` should list it)

## Notes & limitations

- Re-enabling a disabled output restores it as a normal active monitor
  (`preferred, auto, scale 1`). If it was previously mirroring, re-add the
  mirror from `~/.config/hypr/monitors.conf` + `hyprctl reload`.
- Some monitors silently drop occasional DDC writes; nudge the slider again
  if a change doesn't stick.
- Brightness changes are applied per target; "both screens at once" in
  mirror mode is intentionally left to the user so levels stay independent.

## Remove

```sh
omarchy plugin remove io.github.knappkevin.mirror-brightness-display
```

## License

MIT — see [LICENSE](LICENSE).
