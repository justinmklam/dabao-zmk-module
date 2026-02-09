# zmk-config

This repository contains configuration, custom shield files, and keymaps for all my keyboards.

## Building via Github Actions

Firmware is built via Github Actions, and can be downloaded via the artifacts. This avoids needing to set up a local toolchain.

## Building Locally

To build the firmware locally for ease of development, you'll need to set up the ZMK development environment. Follow the [ZMK Setup Guide](https://zmk.dev/docs/development/local-toolchain/setup/native) to get started.

```bash
source ~/zephyrproject/.venv/bin/activate
cd ~/zmk/app
```

Once you have the environment set up, set this `zmk-config` repo as a permanent CMake argument with:

```bash
west config build.cmake-args -- -DZMK_CONFIG=/abs/path/to/zmk-config
```

Now you can build the firmware for a specific keyboard by running:

```bash
# Optionally, use `west build -p ...` for pristine/clean builds
west build -b <board> -d build/<board> -- -DSHIELD=<shield>
```

Replace `<board>` with the name of the board (e.g., `nice_nano`) and `<shield>` with the name of the shield (e.g., `dabao`). The table below shows specific build commands for each keyboard in this repo:

| Board/Shield | Command |
|--------------|---------|
| dabao   | `west build -b nice_nano -- -DSHIELD=dabao -DZMK_EXTRA_MODULES=/abs/path/to/kb_zmk_ps2_mouse_trackpoint_driver/` |

## Flashing Firmware

For the nice!nano, simply double tap the reset button to put it into bootloader mode, then copy the .uf2 file from the build directory to the mounted drive.

```sh
cp ~/zmk/app/build/zephyr/zmk.uf2 /media/$USER/NICENANO/
```
