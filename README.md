<picture align="center">
  <source media="(prefers-color-scheme: dark)" srcset="/docs/images/TOTEM_logo_dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="/docs/images/TOTEM_logo_bright.svg">
  <img alt="TOTEM logo" src="/docs/images/TOTEM_logo_dark.svg">
</picture>

<h1 align="center">T O T E M</h1>

TOTEM is a 38 key column-staggered choc split keyboard. It is meant to be used with a [Seeed Studio XIAO nRF52840 BLE](https://www.seeedstudio.com/Seeed-XIAO-BLE-nRF52840-p-5201.html) or [XIAO RP2040](https://www.seeedstudio.com/XIAO-RP2040-v1-0-p-5026.html).
It was created for the SEEED XIAO keyboard contest.\
[Here](https://www.hackster.io/geist/totem-a-tiny-splitkeyboard-with-splay-cb2e43) you can read about the process of making it.

***

## LAYOUT

![TOTEM layout](/docs/images/TOTEM_layout.svg)

***

## 42-KEY VARIANT (WORK IN PROGRESS)

This fork adds four keys to the TOTEM: one key above each outer pinky key (same 10° tilted column, one 17 mm pitch up) and one extra outer thumb key per side (continuing the thumb arc at 15°). The new keys form a sixth matrix column on XIAO pin D7 (`P1.12`, the former TRRS RX line), so this variant is meant for a wireless build with the XIAO nRF52840, where the TRRS jack is not populated.

What is done in the KiCad project ([PCB/totem_0-3](/PCB/totem_0-3/)):

- schematic: `SWL20/SWL21`, `SWR20/SWR21` with diodes `DL20/DL21`, `DR20/DR21` on `COL5_L`/`COL5_R`, XIAO pin 8 relabelled from `RX` to `COL5`, TRRS RX pin marked no-connect
- PCB: the switch and diode footprints are placed with their nets assigned, and the old RX traces are removed

What is still left to do in KiCad before ordering boards:

- route `COL5_L`/`COL5_R` and the four new diode nets, and re-route the existing tracks that now run under the new footprints
- extend the board outline (`Edge.Cuts`) around the new pinky and thumb keys, then refill the ground zones
- move the back-side silkscreen text that now sits under the new left thumb key
- regenerate the Gerbers and PDFs; the case STEP files also need to be re-modelled for the larger outline

Firmware for this variant is an [RMK](https://rmk.rs/) project in [firmware/RMK/totem](/firmware/RMK/totem/).

***

## PCB

[Here](/PCB/) you can find the KiCad files and Gerbers for the TOTEM.

***

## CASE

You can use the TOTEM without a case, but [here](/case/) you can find one I made for it.

***

## BUILD GUIDE

The build guide for the TOTEM can be found [here](/docs/buildguide.md).

***

## FIRMWARE

[QMK (VIAL) precompiled](/firmware/QMK/) or [QMK (VIAL) source](/firmware/QMK/VIAL_source/) for the TOTEM (wired using the XIAO RP2040)\
[ZMK precompiled](/firmware/ZMK/) or [ZMK source (outdated)](https://github.com/GEIGEIGEIST/zmk-config-totem) for the TOTEM (wireless using the XIAO BLE)\
[RMK source](/firmware/RMK/totem/) for the 42-key variant (wireless using the XIAO nRF52840)

***

## BUY

You can buy TOTEM kits and finished builds on [keeb.supply](https://keeb.supply/products/geist-totem) (based in Germany)

***

## PHOTOS

This is the TOTEM in a black resin case

![TOTEM black resin](/docs/images/TOTEM_black_perspective.jpg)\
![TOTEM black resin](/docs/images/TOTEM_black_top.jpg)\
![TOTEM black resin](/docs/images/TOTEM_black_bottom.jpg)

This is the TOTEM with a black resin tenting bottom plate

![TOTEM black resin tenting](/docs/images/TOTEM_black_tenting_example.jpg)\
[Video by *Wolfgang's Channel* showing the tenting system in action](https://youtu.be/rvM2BthjEI4?si=mTJVdPeZstshnDyo)

***

## CREDITS

### INSPIRATION

I've added the additional pinky key to make the TOTEM compatible with the layout boards like the [Balbuzard](https://github.com/brow/balbuzard) by [Tom Brow](https://github.com/brow) and the [Osprette](https://github.com/smores56/osprette) by [Sam Mohr](https://github.com/smores56) use, where you put the keybinding of the top left and right keys on an outer pinky key.

### HELP FIXING THINGS

People who helped me create this board and fix stuff

#### PCB
- [Marco "Bob"](https://github.com/GroooveBob)

#### CASE
- [Freya](https://github.com/freya-irl)
- [Bubbleology](https://github.com/bubbleology)

#### FIRMWARE
- [Cem Aksoylar](https://github.com/caksoylar)
- [Grinnie](https://github.com/regicidalplutophage)
- [Alaa Saad Mansour](https://github.com/AlaaSaadAbdo)
- [pekudzu](https://github.com/pekudzu)


If you build a TOTEM I would be pretty happy to see some pictures. And if you want to leave me a tip you can do this [here](https://ko-fi.com/geigeigeist) (but please don't feel pressured)
