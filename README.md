## ZMK config for Charybdis

This repository provides firmware for the wireless hot-swap Charybdis customized by MiaoMiao, while keeping compatibility with the official soldered version.

Keys can be remapped in the browser with the [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/).

## Troubleshooting: "flashes fine but keyboard does not work"

If flashing appears successful but the keyboard is unresponsive, check the following in order.

### 1) Hardware sanity checks

- Use a known-good **data** USB cable (many cables are charge-only).
- Try another USB port/computer.
- Confirm each half powers on (LED/bootloader behavior).
- If one half works and the other does not, the issue is likely that half's wiring, MCU, or firmware file.

### 2) Flashing pitfalls (most common)

This repo builds 3 artifacts in `firmware.zip`:
- `charybdis_left` (for left half)
- `charybdis_right` (for right half)
- `settings_reset` (to clear stored Bluetooth/settings)

Common mistakes:
- Flashing `left` firmware to the right half (or vice versa).
- Flashing only one half.
- Not entering bootloader mode correctly (usually double reset).
- Using a file format not supported by your bootloader (`.uf2` vs `.hex`).

If in doubt:
1. Flash `settings_reset`.
2. Re-enter bootloader.
3. Flash the correct left/right image to each half.
4. Power-cycle both halves and pair again.

### 3) Spanish layout/keymap concerns

Being Spanish is **not** a reason for the keyboard to be dead/unresponsive.

- Language/layout mismatches (ES vs US host layout) usually cause **wrong symbols** (for example `;`, `'`, `-`, etc.), not a completely dead keyboard.
- This keymap is based on standard HID keycodes. If keys do nothing at all, suspect flashing/hardware/boot issues first.
- To isolate layout issues, test with a default keymap and set your OS layout explicitly (Spanish or US as desired).

### 4) Signs of a deeper firmware/bootloader issue ("bricked" symptoms)

Potential brick/unresponsive signs:
- No key output and no BLE behavior after flashing.
- Device never appears as USB HID after reboot.
- Bootloader drive does not appear even after reset sequence.

Recovery attempts:
- Double-tap reset to force bootloader.
- Flash `settings_reset`, then proper left/right firmware again.
- If bootloader still never appears, inspect hardware (MCU, reset pin, solder joints, battery/voltage).

### 5) CI/build status context for this repo

- Recent successful build run: all matrix jobs for `nice_nano_v2` + `charybdis_left/charybdis_right/settings_reset` completed successfully.
- A newer PR run with `action_required` had no build jobs executed, so it is not evidence of firmware breakage.
