# Project notes

Personal fork of the Kinesis Advantage360 Pro ZMK config, tuned for macOS.
Read this first; update it when anything below changes.

## Repos and build

- Fork: `athinktank/Adv360-Pro-ZMK`, branch `V3.0`. `upstream` is Kinesis.
- `gh` defaults to the upstream repo here. Always pass
  `-R athinktank/Adv360-Pro-ZMK`, or runs and artifacts won't show up.
- Every push to `V3.0` runs `.github/workflows/build.yml`. Only the
  `build-clique` job runs (the legacy job has `if: false`). The artifact is
  `firmware-clique`.
- Download into the repo:
  `rm -rf firmware-clique && gh run download <id> -R athinktank/Adv360-Pro-ZMK -n firmware-clique -D firmware-clique`
- The keymap source is `config/adv360.keymap`. `config/keymap.json` is for
  the web editors and isn't used by the build.

## Current layout choices (Base and Keypad layers)

- Caps Lock key position (left of `A`): Caps Lock. Fn layer has Caps there too.
- Bottom row, left of Left Arrow: Escape.
- Thumbs: Left Alt (Option), Left GUI (Command) on the left; Right GUI,
  Right Alt on the right.
- Right thumb key that was Page Down: Right Control.

## Physical keys

- Mod: top key of the right inner column, left of `6` (`&mo 3`).
- macro1: middle key of the left inner column, right of `T`.
- macro3: middle key of the right inner column, left of `Y`.

| Action | Keys |
|---|---|
| Left half bootloader | Hold Mod, press macro1 |
| Right half bootloader | Hold Mod, press macro3 |
| Unlock for Studio/Clique | Hold Mod, press the key left of `A` |

Fallback: double-press the half's reset button (User Manual section 2.7).

## Flashing

1. Turn the left half on and plug it in over USB. Mod + macro1. Drive `ADV360PRO` mounts.
2. `cp firmware-clique/*-left.uf2 /Volumes/ADV360PRO/`
3. Unplug, turn both halves off, turn the left half back on.
4. Plug in the right half. Mod + macro3.
5. `cp firmware-clique/*-right.uf2 /Volumes/ADV360PRO/`
6. Unplug the right half and turn it on.
7. In the keymap app, restore stock settings (see below).

## Keymap apps (ZMK Studio)

- Use Kinesis Clique: https://clique.kinesis-ergo.com/ (Kinesis-branded ZMK
  Studio). Use Chrome or Edge (needs Web Serial) and USB on the left half.
  ZMK Studio at https://zmk.studio/ also works but isn't the one we use.
- Edits made in the app are saved on the keyboard and override the compiled
  keymap. Flashing does not clear them. After flashing, unlock and use the
  app's restore-stock-settings option, or the new build won't take effect.
