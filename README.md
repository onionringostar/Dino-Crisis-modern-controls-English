# Dino Crisis — Modern controls (PS1, PAL Europe)

English version of nahuelx32's Dino Crisis patch, created by Claude.

A patch for **Dino Crisis** (PlayStation, Europe PAL release, [*SLES-02207*](https://psxdatacenter.com/games/P/D/SLES-02207.html)) that replaces tank controls with modern camera-relative movement and adds an over-the-shoulder third-person camera. It is applied to your own copy of the game; this repository **does not include any part of the game**.

All of the mod's code is in the Euro patch (the same 20 hooks), with one exception: the video skip. So far only booting and the modern controls have been confirmed. Everything else is ported but untested.

## Features

- Free 360° analog movement, relative to the camera. Analog mode is enabled automatically.
- Over-the-shoulder third-person camera (R3 toggles it with the original fixed cameras):
  - the whole room and the dinosaurs are visible, not only what the fixed camera would show;
  - camera changes don't pause the game in shoulder view;
  - lasers and lights are visible from both sides.
- Twin-stick aiming: LT aims, RT fires, the right stick turns the aim.
- Cancelable shots, with a delay between shots similar to the original.
- Auto-run (X toggles it; RB walks). (Inspired by Dino Crisis 2)
- HUD with weapon, magazine/reserve (`EMPTY` = out of ammo) and health; Y toggles it. (Inspired by the VMU display in the Dreamcast version)
- Cutscenes, pushing objects and other actions work as in the original.
- ❌ Start skipping the opening videos: **not working on the European version** (see below).

## Controls

| Button | Action |
|---|---|
| Left stick | move (360°, camera-relative) |
| LT / RT | aim / fire |
| RB (hold) | walk |
| X | toggle auto-run |
| A | action |
| Right stick | shoulder camera; while aiming, turns the aim |
| R3 | shoulder camera ↔ original cameras |
| L3 | camera behind Regina |
| Y | show/hide HUD |

## Port status (Europe PAL)

| Feature | Status |
|---|---|
| Free 360° analog movement, relative to the camera | ✅ Confirmed working |
| Over-the-shoulder camera | ✅ Confirmed working |
| Twin-stick aiming | ✅ Confirmed working |
| Cancelable shots with delay | ⚠️ Ported, untested |
| Auto-run | ✅ Confirmed working |
| HUD (weapon, ammo, health) | ⚠️ Ported with English text, untested |
| Cutscenes, pushing objects and other actions | ⚠️ Ported, untested |
| Start skips the opening videos | ❌ Not working on the European version |

## Notes

- Tested on DuckStation. Not tested on real hardware.
- In very busy shoulder-camera views, some distant scenery may be missing: this is the limit that keeps the game from freezing. Occasionally a door frame, or to a lesser extent other scenery objects, can show through a wall (a limit of the engine's draw order).
- **HUD text:** the Spanish `VACIO` is now `EMPTY`. The other labels (`NONE`, `LIFE`, `SHOTGUN`, `PISTOL`, `SLUG`, `GREN`, etc.) are placeholder choices and can be changed in `dcmod.c`.
- **Video skip:** this relies on addresses inside the video code that is loaded from the disc. Only the Spanish addresses are known, so on the European version the feature does nothing. It is harmless and does not break anything. Finding the European addresses needs a memory dump taken while an intro video is playing.
- **Warning screen:** it cannot be skipped, because that is where the game runs its copy-protection check (same as in the Spanish version).

## Installing

To install, use PPF-O-Matic on your own Europe PAL release, *SLES-02207* disc image.

1. Make a **fresh copy** of your original, unmodified European Track 1 (`.bin`). Never apply the patch on top of an already patched copy.
2. Apply `DinoCrisis_EU_ModernControls_v3_FULL.ppf` to that copy with PPF-O-Matic (it works directly on the `.bin`).
3. Keep the patched `.bin` together with the original `.cue` and the other track files, and make sure the `.cue` points to the patched file's name.
4. Open the `.cue` in your emulator.

## Building from source

Requires Python 3, the `gcc-mipsel-linux-gnu` and `binutils-mipsel-linux-gnu` packages, and `unicorn` (`pip install unicorn`).

```bash
cd eu_src
python3 mkdisc.py "Dino Crisis (Europe) (Track 1).bin" patched.bin
python3 mkppf.py "Dino Crisis (Europe) (Track 1).bin" patched.bin patch.ppf "Dino Crisis EU modern controls"
```

`mkdisc.py` finds the game executable on the disc by itself and verifies it before patching.

Optional environment variables for debugging:

- `DC_ONLY=addr,addr`: install only the listed hooks.
- `DC_SKIP=all` (or a list of addresses): skip all or some hooks.

### Validating loader changes

The Unicorn check built into `mkdisc.py` does not model the real PlayStation CPU's load-delay slot. After any change to the loader, also run:

```bash
python3 chk.py <patched SLES_022.07>
```

This uses `r3k.py`, an interpreter that models load and branch delays.

## How it works

The patch adds a small loader to free space in the game executable. At startup it unpacks the mod's code into RAM at `0x800D8000` and then starts the game normally. A set of hooks in the game code redirect to the mod, which handles movement, camera, aiming and the HUD.

## Legal

The code in this repository is MIT licensed (see [LICENSE](LICENSE)). *Dino Crisis* is © Capcom. No part of the game is included here: no images, executables or disc sectors. You need your own copy.

## Credits

Based on nahuelx32's Spanish Dino Crisis modern-controls mod; this English/PAL Europe port was created by Claude. Auto-run is inspired by Dino Crisis 2, and the HUD by the VMU display in the Dreamcast version.
