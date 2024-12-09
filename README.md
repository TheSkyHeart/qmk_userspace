# My QMK Keymaps

## Features

## How to build with GitHub

✅ Easier. No setup required.

❌ Longer feedback loop. Changes need to go through CI.

1. Push your changes to the remote.

    ```sh
    git push origin main
    ```

2. Wait for the CI to pass. (A GitHub Action will build your firmware.)

    ```sh
    gh run watch
    ```

3. Grab the firmware from the CI artifacts.

    ```sh
    gh run download
    ```

    > ℹ️ Please note that these artifacts are ephemeral and they may be expired if you try to access them later on. You can always grab the latest firmware from the [Releases](https://github.com/mikybars/qmk_userspace/releases) page.

4. Flash the firmware to your keyboard. This depends on your microcontroller. If yours is RP2040 based, take a look at the next section.

## Flashing RP2040 microcontroller

> ⚠️ Please always unplug your keyboard from your computer before removing the TRRS cable!

-   Disconnect TRRS/TRS cable between the splits (keyboard halfs).
-   For each split, do:
    -   Connect your split to the computer using USB.
    -   Press the reset switch of the split two times consequently so that your RP2040 based MCU will go to Bootloader Mode.
    -   You must see Raspberry PI Boot Device in the output of lsusb. It's also detected as Mass Storage Device.
    -   Drag and Drop (cp or copy) the .uf2 file to the RP2040 Mass Storage Device.
    -   After the firmware is copied, you will see that the MCU exits Bootloader mode and Mass Storage Device is no longer present. It means that the firmware is flashed!

## Drawing your keymap

Drawing your keymap can really help you memorize the different layers. Furthermore, it lets others discover your keymap more easily.

The fancy graphics in this repo are custom made. For a more repeatable process I use [keymap-drawer](https://github.com/caksoylar/keymap-drawer).
For example, to generate the sweep `keymap.yaml` file, I ran the following command. It uses `uv` to avoid having to install the tool:

```bash
uvx --from keymap-drawer keymap parse -c 10 -l COLEMAK QWERTY NAV SYM NUM GAME -q keymap.json > sweep_osm.yaml
```

Unfortunately, it does not automatically parse combos. You will have to add those manually. To finally draw the keymap run:

```bash
uvx --from keymap-drawer keymap draw sweep_osm.yaml > sweep_osm_keymap.svg
```

I am also working on a worklfow to automate the drawing.

## My keymaps in detail

Check `docs/generated` for the most up-to-date graphics.
