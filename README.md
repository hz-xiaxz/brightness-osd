# brightness-osd

A lightweight GTK brightness on-screen display for Linux desktops.

`brightness-osd` adjusts screen brightness with `brightnessctl` and shows a centered, translucent OSD with a percentage and progress bar. It is useful on lightweight desktop environments such as XFCE where brightness keys may work but the default visual feedback is missing or notification-based.

## Features

- Centered floating OSD
- Translucent rounded window
- Brightness percentage display
- Progress bar
- Single-instance refresh behavior for repeated key presses
- No Electron or heavyweight runtime
- Works well with XFCE custom keyboard shortcuts

## Requirements

- Linux desktop session with X11/GTK support
- Python 3
- `brightnessctl`
- GTK 3 Python bindings

On Arch Linux / Manjaro:

```sh
sudo pacman -S --needed brightnessctl python-gobject gtk3
```

## Installation

Clone the repository and install the script somewhere in your `PATH`:

```sh
git clone https://github.com/hz-xiaxz/brightness-osd.git
cd brightness-osd
chmod +x brightness-osd
mkdir -p ~/.local/bin
cp brightness-osd ~/.local/bin/
```

Make sure `~/.local/bin` is in your `PATH`.

## Usage

Increase brightness:

```sh
brightness-osd up
```

Decrease brightness:

```sh
brightness-osd down
```

The first call starts a small background OSD process. Repeated calls update the same floating window instead of creating stacked notifications.

## XFCE keyboard shortcuts

In XFCE, bind your brightness keys to:

```sh
brightness-osd down
brightness-osd up
```

For example, you can bind:

- `F1` or `XF86MonBrightnessDown` to `brightness-osd down`
- `F2` or `XF86MonBrightnessUp` to `brightness-osd up`

You can also configure them with `xfconf-query`:

```sh
xfconf-query -c xfce4-keyboard-shortcuts -n -t string -p '/commands/custom/F1' -s 'brightness-osd down'
xfconf-query -c xfce4-keyboard-shortcuts -n -t string -p '/commands/custom/F2' -s 'brightness-osd up'
xfconf-query -c xfce4-keyboard-shortcuts -n -t string -p '/commands/custom/XF86MonBrightnessDown' -s 'brightness-osd down'
xfconf-query -c xfce4-keyboard-shortcuts -n -t string -p '/commands/custom/XF86MonBrightnessUp' -s 'brightness-osd up'
```

If your desktop environment does not include `~/.local/bin` in shortcut command lookup, use the full path instead:

```sh
/home/your-user/.local/bin/brightness-osd up
/home/your-user/.local/bin/brightness-osd down
```

## Notes

`brightness-osd` uses a Unix socket under `XDG_RUNTIME_DIR` to communicate with the background OSD process. This keeps repeated key presses smooth and prevents notification stacking.

## License

MIT License. See [LICENSE](LICENSE).
