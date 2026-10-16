English version of nahuelx32's Dino Crisis patch created by Claude

To install use PPF-o-Matic on your own Europe PAL release, *SLES-02207* disc image
https://psxdatacenter.com/games/P/D/SLES-02207.html


<a name="english"></a>
# Dino Crisis — Modern controls (PS1, PAL Europe)



A patch for **Dino Crisis** (PlayStation, Europe PAL release, *SLES-02207**) that replaces tank controls with modern camera-relative movement and adds an over-the-shoulder third-person camera. It is applied to your own copy of the game; this repository **does not include any part of the game**.


## Features

- Free 360° analog movement, relative to the camera. Analog mode is enabled automatically.
- Over-the-shoulder third-person camera (R3 toggles it with the original fixed cameras):
  - the whole room and the dinosaurs are visible, not only what the fixed camera would show;
  - camera changes don't pause the game in shoulder view;
  - lasers and lights are visible from both sides.
- Twin-stick aiming: L2 aims, R2 fires, the right stick turns the aim.
- Cancelable shots, with a delay between shots similar to the original.
- Auto-run (Square toggles it; R1 walks). (Inspired by Dino Crisis 2)
- HUD with weapon, magazine/reserve (`VACIO` = out of ammo) and health; Triangle toggles it. (Inspired by the VMU display in the Dreamcast version)
- Start skips all opening videos. The warning screen at startup can't be skipped: that's where the game runs its copy-protection check.
- Cutscenes, pushing objects and other actions work as in the original.

## Controls

| Button | Action |
|---|---|
| Left stick | move (360°, camera-relative) |
| L2 / R2 | aim / fire |
| R1 (hold) | walk |
| Square | toggle auto-run |
| X | action |
| Right stick | shoulder camera; while aiming, turns the aim |
| R3 | shoulder camera ↔ original cameras |
| L3 | camera behind Regina |
| Triangle | show/hide HUD |



**Notes:**

- Tested on DuckStation. Not tested on real hardware
- In very busy shoulder-camera views, some distant scenery may be missing: this is the limit that keeps the game from freezing. Occasionally a door frame, or to a lesser extent other scenery objects, can show through a wall (a limit of the engine's draw order).



## Legal

The code in this repository is MIT licensed (see [LICENSE](LICENSE)). *Dino Crisis* is © Capcom. No part of the game is included here: no images, executables or disc sectors. You need your own copy.
