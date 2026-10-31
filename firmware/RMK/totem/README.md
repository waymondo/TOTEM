# TOTEM 42-key, RMK firmware (XIAO nRF52840, BLE split)

[RMK](https://rmk.rs/) firmware for the 42-key TOTEM variant: the 38-key TOTEM plus one key above each outer pinky key and one extra outer thumb key per side. Both halves use a Seeed XIAO nRF52840 and talk to each other over BLE; the left half is the central (pairs with the host), the right half is the peripheral.

Everything is driven by `keyboard.toml`:

- matrix: 4 rows x 6 cols per half, diodes COL2ROW. Column 5 is the new column on XIAO pin D7 (`P1_12`, formerly the TRRS RX line). The TRRS jack is not populated on a BLE build.
- layout / keymap: 5 layers ported from the QMK default keymap (qwerty, colemak, lower, raise, adjust). The four new keys default to Tab / Quote (above the pinkies) and Escape / Delete (outer thumbs); change them in `keyboard.toml` or live in Vial.
- `vial.json`: Vial layout definition for the 4x12 unified matrix (left = cols 0-5, right = cols 6-11).

## Build

Install Rust, the Cortex-M4F target and the helper tools once:

```shell
rustup target add thumbv7em-none-eabihf
cargo install cargo-make cargo-binutils flip-link cargo-hex-to-uf2
rustup component add llvm-tools
```

Then build both halves as UF2 files:

```shell
cargo make uf2 --release
```

This produces `rmk-central.uf2` (left) and `rmk-peripheral.uf2` (right). `cargo build --release --bin central` / `--bin peripheral` builds the ELF files only.

## Flash

The XIAO nRF52840 ships with the Adafruit nRF52 UF2 bootloader, which is what `memory.x` assumes (flash starts at `0x1000`). Double-tap the reset button, a `XIAO-SENSE`/`XIAO-BOOT` drive appears, copy the matching UF2 onto it. Flash the left half with `rmk-central.uf2` and the right half with `rmk-peripheral.uf2`.

If you have previously run ZMK on the same XIAOs, clear the settings area once (flash the ZMK `settings_reset` UF2, or hold the adjust-layer "clear peer" key for 5 s after flashing RMK) so stale bonds do not interfere with pairing the halves.

## Notes

- Battery level reporting is disabled. The XIAO's battery divider on `P0_31` has to be enabled by pulling `P0_14` low, which RMK's plain `battery_adc_pin` setting cannot do.
- `ble_addr` is not set because RMK derives the address from the nRF52's factory ID.
- The project is a copy of RMK's `examples/use_config/nrf52840_ble_split` with the TOTEM matrix, layout and keymap filled in. It has not yet been compiled from this repository; if a newer RMK release changes the `keyboard.toml` schema, follow the error messages or diff against the current upstream example.
