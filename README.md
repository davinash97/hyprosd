# hyprosd

![hyprosd screenshot](assets/example.png)

Simple Hyprland OSD for volume, brightness, Caps Lock, and Num Lock.

[View on AUR -->](https://aur.archlinux.org/packages/hyprosd-git)

## Install

```bash
yay -S hyprosd-git
# or
paru -S hyprosd-git
```

Manual:

```bash
git clone https://github.com/jameswylde/hyprosd.git
cd hyprosd
chmod +x ./scripts/install.sh
./scripts/install.sh
```

## Hyprland config

Start the daemon:

```
exec-once = hyprosd daemon
```

For manual installs:

```
exec-once = ~/.local/bin/hyprosd-daemon
```

Example keybinds (using `wpctl` and `brightnessctl`):

```
bind = ,XF86AudioLowerVolume, exec, wpctl set-volume @DEFAULT_AUDIO_SINK@ 5%- && hyprosd show volume
bind = ,XF86AudioRaiseVolume, exec, wpctl set-volume @DEFAULT_AUDIO_SINK@ 5%+ && hyprosd show volume
bind = ,XF86AudioMute, exec, wpctl set-mute @DEFAULT_AUDIO_SINK@ toggle && hyprosd show volume
bind = ,XF86MonBrightnessDown, exec, brightnessctl s 10%- && hyprosd show brightness
bind = ,XF86MonBrightnessUp, exec, brightnessctl s +10% && hyprosd show brightness
```

## Theming

The OSD follows your desktop's light/dark preference (`org.gnome.desktop.interface color-scheme`), switching between a dark and a light palette accordingly. Shape, sizing, icons, and corner radius are unaffected — only the colors adapt. If that preference can't be read, it falls back to the original dark/translucent look.

The volume/brightness bar fill uses an accent color (default `#247be0`), the same in both light and dark mode. It's not read from the system automatically (GTK/GNOME don't expose a reliable way to query it outside a full desktop session) — it's set via `ThemeConfig::accent` in `src/config.rs` until file-based config loading lands.

Blur rules:

```
layerrule = blur on, match:namespace hyprosd
layerrule = ignore_alpha 0.1, match:namespace hyprosd
```

## Uninstall

```bash
sudo pacman -R hyprosd-git
```

Manual installs:

```bash
./scripts/uninstall.sh
```
