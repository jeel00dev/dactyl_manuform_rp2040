# Jeel00dev — Custom 5x6_5 Handwired Keyboard (RP2040 Zero)

Welcome, this repo documents my custom handwired keyboard project built around the **RP2040 Zero** MCU.  
Layout: **5x6_5** (handwired Dactyl/Manuform style). Firmware files and keymap are in:

```

qmk/keyboards/handwired/dactyl\_manuform/5x6\_5/keymaps/jeel00dev

```

This README shows how to use the repo, install dependencies, build the QMK firmware, and flash it to an RP2040 Zero. Check the `photos/` folder for soldering and wiring reference images.

---

## Repo structure

```

my\_keyboard/
├── photos/
├── qmk_firmware/
├── requirements.txt
├── README.md
├── stl_model ( for 3d pront )

```

---

## Project highlights

- **Microcontroller:** RP2040 Zero
- **Layout:** 5x6_5 handwired (rows × columns with thumb keys)
- **Keymap folder:** `qmk_firmware/keyboards/handwired/dactyl_manuform/5x6_5/keymaps/jeel00dev`
- **Photos:** See `photos/` for soldering, wiring, and assembly images, use these for reference when building.

---

## Requirements & Dependencies

This project requires Python 3 and the QMK toolchain (via the `qmk` Python package) plus a few helper packages. I included a `requirements.txt` with the exact packages used for development.

To install the Python dependencies:

```bash
# from your repo root
python3 -m pip install --user -r requirements.txt
```

`requirements.txt` contains the packages used during development:

```
argcomplete==3.6.2
attrs==25.3.0
colorama==0.4.6
dotty-dict==1.3.1
halo==0.0.31
hid==1.0.8
hjson==3.1.0
jsonschema==4.25.1
jsonschema-specifications==2025.4.1
log-symbols==0.0.14
milc==1.9.1
Pillow==11.3.0
pip==25.2
platformdirs==4.3.8
Pygments==2.19.2
pyserial==3.5
pyusb==1.3.1
qmk==1.1.8
referencing==0.36.2
rpds-py==0.27.0
six==1.17.0
spinners==0.0.24
termcolor==3.1.0
types-colorama==0.4.15.20250801
```

### System prerequisites (examples)

- `git`
- `python3` (3.8+ recommended)
- `pip` (for Python package installs)

---

## How to flash the RP2040 Zero

There are two common ways to flash RP2040 boards:

### Method 1 — Automatic: `qmk flash`

If your local QMK setup supports automatic flashing, `qmk flash` will compile and attempt to flash the board:

```bash
# compile + flash (qmk will usually prompt you to put the MCU in bootloader mode)
qmk flash -kb handwired/dactyl_manuform/5x6_5 -km jeel00dev
```

**Procedure:**

1. Run the command above.
2. When prompted, put your RP2040 Zero into BOOTSEL/bootloader mode:
   - **Hold the BOOTSEL button** (or the specific boot button on your board) while plugging the USB cable into the board.
   - The board should appear as a USB mass storage device (on desktop OSes) or be recognized by the QMK tool.

3. QMK will try to flash the compiled firmware. Follow on screen prompts.

`qmk flash` is convenient because it hides the low-level flashing details for you.

---

### Method 2 — Manual UF2 copy

RP2040-based boards often support flashing via a UF2 file:

1. Compile the firmware (see compile step above). Note where QMK outputs the artifact (look for `.uf2` in qmk_firmware/.build/ output).
2. Put the RP2040 Zero into BOOTSEL (hold BOOTSEL while plugging in to laptop
   wia usb).
3. The board shows up as a removable drive (like `RPI-RP2` in file explorer).
4. Copy the `.uf2` file to that drive (drag & drop).
5. The board will reboot and run the new firmware.

---

## Photos & wiring / soldering reference

Check the `photos/` folder for:

- soldering closeups
- switch wiring
- TRRS/TRS/USB wiring
- thumb cluster wiring
- https://medium.com/swlh/complete-idiot-guide-for-building-a-dactyl-manuform-keyboard-53454845b065 ( detailed guide for wiring dactyl_manuform )

---

## Customization & editing the keymap

- To change key assignments, edit `qmk_firmware/keyboards/handwired/dactyl_manuform/5x6_5/keymaps/jeel00dev/keymaps.json` in that keymap folder.
- After editing, re-run `qmk compile` (or `qmk flash`) to build the updated firmware.

---

## Troubleshooting

- **Board not detected in bootloader mode:** Ensure you press/hold the BOOTSEL button **before** plugging the board in. Try a different cable or USB port.
- **Compile errors:** Make sure you copied the keyboard/keymap files into a compatible `qmk_firmware` version.
- **Wrong pins or wiring mistakes:** Double check photos and `config.h` pin mappings in the keymap folder.
- **Permission errors on Linux:** You may need `sudo` for some USB operations or set up udev rules.

---

## How I use this repo

1. Clone this repo.
2. `pip install --user -r requirements.txt`
3. `qmk compile -kb handwired/dactyl_manuform/5x6_5 -km jeel00dev`
4. `qmk flash -kb handwired/dactyl_manuform/5x6_5 -km jeel00dev` (or manual UF2 copy)

---

## License & credits

- Project: QMK Firmware
- Repository: https://github.com/qmk/qmk_firmware
- If you use this as a base for your own project, please give a link back, I’d love to see what you build.

---

## Questions / Issues

If you find problems or want to suggest improvements, open an issue on this repo or contact me via GitHub.

---
