# barpop

SwiftUI popups for [SketchyBar](https://github.com/FelixKratz/SketchyBar) on
macOS: calendar and agenda, media, volume, Wi-Fi, Bluetooth, battery, weather,
performance and wallpaper. It runs as a daemon beside sketchybar and opens a
popup under the bar item that asks for it.

## Build

```bash
git clone https://github.com/nhalm/barpop ~/.local/share/barpop
make -C ~/.local/share/barpop
```

Needs the Xcode command line tools (`swiftc`). The build is an ad-hoc signed
app bundle, `bin/barpop.app`, so macOS asks for Calendar, Bluetooth and
Location access in barpop's own name. `bin/barpop` is the same binary for the
CLI commands.

## Develop

`make setup` installs the git hooks (`lefthook.yml`: gitleaks on staged
changes; versions in `mise.toml`). Needs mise.

## Use

```bash
barpop daemon <sketchybar-pid>                         # started by the sketchybar config
barpop show <popup> '<x,y,w,h;...>' <item> [keyboard]  # open a popup under an item
barpop hide                                            # close the open popup
barpop sync                                            # re-send current state to the bar
```

barpop triggers these sketchybar events: `barpop_popup` (ITEM, OPEN=1/0),
`barpop_media`, `barpop_network`, `bluetooth_change`.

The sketchybar side lives in
[nhalm/dotfiles](https://github.com/nhalm/dotfiles) at
`macos/.config/sketchybar/helpers/barpop.lua`.

## Expects

- `~/.local/state/matugen/barpop.json`: palette from the `matugen/barpop.json` template
- `~/.config/sketchybar/helpers/location.sh`: cached CoreLocation fix, for weather
- `~/.local/scripts/wallpaper.sh`: applies a wallpaper chosen in the picker

## Design

[`DESIGN.md`](DESIGN.md) describes the component kit in `Kit/`.

## Licence

MIT
