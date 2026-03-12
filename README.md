# raw-keys-waynergy

Raw keycode mapping for Waynergy — Mac keyboard to Linux (GNOME/Wayland + uinput)

---

## Background

The native Synergy and Barrier clients do not support Wayland. As a workaround,
waynergy can be used as a Wayland-native client. However, GNOME's
implementation requires raw input mode via uinput, which means Synergy's
built-in key translation is bypassed entirely.

This repository provides a [raw-keymap] configuration that maps the raw keycodes
sent by a macOS Barrier server to the correct Linux uinput keycodes on the
client side.

---

## Problem

When using waynergy with uinput on GNOME:
  - uinput does not support xkb keymaps
  - Raw keycodes from macOS differ from Linux keycodes
  - Without a mapping, most keys register incorrectly or not at all

---

## Solution

A [raw-keymap] section in ~/.config/waynergy/config.ini maps each
Mac Barrier server keycode to its corresponding Linux uinput keycode.

Format:
  remote_keycode = local_keycode

Example:
  [raw-keymap]
  98  = 111   # Mac Page Up  → Linux KEY_UP
  100 = 113   # Mac Left     → Linux KEY_LEFT
  102 = 114   # Mac Right    → Linux KEY_RIGHT
  104 = 116   # Mac Page Dn  → Linux KEY_DOWN

---

## Setup

1. Install waynergy:
     https://github.com/r-c-f/waynergy

2. Configure waynergy to use uinput in ~/.config/waynergy/config.ini:
     [input]
     method = uinput

3. Copy the [raw-keymap] section from this repository into your config.

4. Restart waynergy and test your keys.

---

## Generating Your Own Mapping

If your setup differs, use waynergy-mapper to generate a custom mapping:

  waynergy-mapper -r

This iterates through local keycodes and records the remote codes as you
press each key on the Barrier server — similar to xev/wev but with
immediately usable config output.

---

## Environment

  Server:   macOS with Barrier
  Client:   Linux (GNOME, Wayland)
  Input:    uinput (raw-keymap)

---

## References

  - waynergy:  https://github.com/r-c-f/waynergy
  - Barrier:   https://github.com/debauchee/barrier

---

## License

MIT
