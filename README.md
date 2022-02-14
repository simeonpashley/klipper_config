# klipper_config
Klipper config for Creality Ender 3 V2

Tweaked to suit printer & my needs.

# Shopping List

## Main parts
- Creality Ender 3 V2 - https://amzn.to/3AKjhfT
- E3D Hemera 24v - https://amzn.to/34miju6
- E3D Hemera metal backplate - https://amzn.to/3uasRaJ
- CR Touch - https://amzn.to/3KRwpEJ
- Dual Z-axis Upgrade Kit - https://amzn.to/34mhlhs
- BIGTREETECH SKR 2 Motherboard with 5x TMC2209 - https://amzn.to/3AMYY1j
- Bed compression springs - https://amzn.to/3KWfjp6
- 4010 Noctua 12v fan (2 of) - https://amzn.to/3geOgHz
- 92mm Noctua 12v fan (2 of) - https://amzn.to/3uf4ngr
- 5015 24v blower fans - https://amzn.to/3HbUYd8

## Filaments
- eSun PLA+ - https://amzn.to/3AKjHmt
- Hatchbox PETG - https://amzn.to/3IRHpjv
- Evyone PETG (Hatchbox is better) - https://amzn.to/3reZgLp
- Creality PLA (eSun PLA+ is better) - https://amzn.to/3HjlEbX

## Extras
- JST Connector kit - https://amzn.to/3KXofdX
- Washers - https://amzn.to/3gdb8as
- 26AWG Wire - https://amzn.to/3g7UTvj
- M3 bolts & nuts (big size range) - https://amzn.to/3AJkGmS
- M3 square nuts - https://amzn.to/32JmUGe
- M2-2.5 screws - https://amzn.to/34q0Wc1
- M3-M5 bolts & nuts - https://amzn.to/34o6vHD
- Dupont pins & crimper - https://amzn.to/3AJGK0C
- Buck converters - https://amzn.to/3odvViq
- Heat shrink tubing - https://amzn.to/345HEsy
- Tie wraps - https://amzn.to/3IO6yeU

# Build
2022-02-05
- Published current mounts at Thingverse https://www.thingiverse.com/thing:5233293

2022-02-01
- Dual Z screw split into 2 cables - "z" for left/stock & "z1" for right screw. Attached to E1 port on SKR
- Config for dual z `Z_TILT`, run_currents, etc.

2022-01-30
All working config for
- Creality Ender 3 V2
- BigTreeTech SKR 2 - klipper
- Raspberry Pi Zero 2 W (with colour coded header) with GPIO & +5v from SKR
- Mainsail
- CR Touch
- Hemera Direct Drive Extruder
- Dual Z screw after installing heavyweight Hemera - cable splitter and ONE connection to board. To be split later.

2022-01-26
- WIP - migrating to BTT SKR2 & Mainsail (from stock & octopi `./octopi`)

2022-01-??
- Dual Z screw kit via Amazon. Tricky to install and requires some Z-axis stepper cable routing around the back of the PSU as the existing cables are ultimately very short and don't reach. Provided Z-Split cable goes down back of PSU, then joins up to existing cable near mother board.

2022-01-01
- Hemera Direct Drive upgrade
- Noctua 4010+Buck on Hemera after I caught the stock Hemera fan and snapped a blade :'(
- Swapped to Hemera metal backplate from Amazon as the printed one had flex despite ribs & 85% fill. The metal backplate isn't great but it's rigid.
- Provided Hemera thermistor and heat cables are too short when the extruder is at X=max, Y=min, Z=max for a reasonable run into the controller board so had to hack the covers and ultimately bring those cables around the side. Still short but it _just_ works.

Hemera: Printed backplate, fan duct, and attachments

2021-12-01
- Replaced all fans with Noctua variants and buck converters to reduce noise. CPU cover, PSU cover, "Briss moto" cooling w/ 2x Noctua 4010 and riser feet

## Hemera install
"Dry fit" all components & parts for complete Hemera install before I did it.
You will need a wide selection of M3 bolts, nuts & washers from 5mm up to 22mm
Be prepared for electronics, wiring, soldering, etc.
Most online guides/videos are made by people with multiple printers so they can print parts if required during the build. If, like most people, you have 1 printer then test everything before you touch your working printer.
I printed various backplates, ducts, connectors, adapters, and test-fitted them all to the Hemera before I actually dismantled the printer and rebuilt it.

Things of note
- X-end stop hitting various backplates during Hemera required mods to those
- Most backplates are built for BL Touch

### Hemera retraction
Retraction 0.3mm at 45mm retract, 25mm detract.
BEWARE that if your detract speed is too high, you get gaps on the model exactly where the "detraction"s are shown in Prusaslicer.

# Software
Started using Cura, moved to Prusaslicer v2.4+ for finer control.
Fusion 360 for STL mods

- Prusaslicer bug where "Gap Speed">0 breaks all Auto Volume speeds. Appears when you try and use Volumetric Speed and no changes occur. https://github.com/prusa3d/PrusaSlicer/issues/6844

# BTT SKR V2
w/ 5 x tmc2209

Board does not fit inside 1 side of the under-carriage so dedicated left & right carriages are required to host it.
The USB-A cable protrudes a long way, so take that into account. A rPI connected via GPIO will save a lot of space and negate the need for the USB.

For klipper, go through the checks carefully.
https://www.klipper3d.org/Config_checks.html

Especially, `STEPPER_BUZZ` command will save a lot of grinding and things going in the wrong direction. e.g., `STEPPER_BUZZ STEPPER=stepper_x`

For me, the `[tmc2209 stepper_???]` sections were important as without them the steppers ran the wrong distances.

## Stepper End stops
SKR has 3-pin stops whereas the Stock has 2-pin stops. Inside the 3-pin male, push the 2-pin female in at the end away from the steppers. I used side-cutters to strip the tiny outer alignment shims to get a good fit without spraining the board.

## CR Touch
CR Touch wiring, VERY different from BL Touch. **Be careful!! Pretty much reversed!! I fried a CR touch with the wrong wiring!!!**

Split the 5-wire female JST into a 3 & 2. I carefully retracted the pins from the 5-block and pushed them into 2 new blocks as below

### CR touch - reference
https://www.reddit.com/r/BIGTREETECH/comments/pjrkj2/crtouch_wiring_for_btt_skr_v14_and_skr_v2/

https://www.reddit.com/r/Creality/comments/pl4fyv/creality_cr_touch_wiring_diagrampinout/

Reminder graphic here: https://imgur.com/a/39DU1cv

### Creality board 5-pin JST block

|COLOUR |stock board label |PIN |SKR |
--- | --- | ---| ---|
|White |G |GND |GND |
|Black |V |+5V |+5V |
|Yellow |IN |PB0 SIG |PE5 |
|Red |G |GND |GND |
|Blue	|OUT |PB1 SIG |PE4 |

### SKR JST blocks

   3-pin sensor     ~ 2-pin probe
   |3A |3B |3C |~ |2A |2B |
--- | --- | ---| ---| ---| ---|
|wht |blk |yel |~ |red |blu |
|GND |+5V |PE5 |~ |GND |PE4 |

## Steppers
When installing, needs the X stepper direction inverting from stock config by putting a `!` at the start of the Klipper config.

`dir_pin: !PE1 ; this is inverted with the "!" from the stock board`

Make sure the config has the appropriate tmc2209 blocks are the distance will be wrong
e.g., `[tmc2209 stepper_x]`

## Raspberry PI
ref: https://www.reddit.com/r/3Dprinting/comments/n73s1j/pi_zero_w_klipper_fluidd_mainsail_guide_skr_mini/
YMMW: Don't use this literally but as a general guide, config changes are required.

Connect RPI via GPIO to remove the need for a massive USB-A cable

(@RPi) GP6  => (@SKR - TFT) GND, 2nd pin from left (steppers at top)
(@RPi) GP10 => (@SKR - TFT) PA9, TFT 3rd pin from left (middle)
(@RPi) GP8  => (@SKR - TFT) PA10, 4th pin from left

My wiring

|rpi |colour| skr|
| ---| ---| ---|
|GP6 |black| pin 2|
|GP10 |gray| pin 3|
|GP8 |white| pin 4|


https://github.com/bigtreetech/SKR-2/issues/13#issuecomment-831507297

```
On SKR-2 PA9 is TX and PA10 is RX. So pin 10 (RXD0) of RPi would go to the middle pin (PA9) of TFT connector on SKR-2 and pin 8 (TXD0)of RPI would go to the 4th pin from left (PA10) on tft connector. And then or course, pick any ground pin on rpi and connect to second pin over from left (GND) on SKR-2.
```

For my setup, RPI Zero 2, only connected over `/dev/serial0` as the documented `/dev/ttyAMA0` did not work at all for me.

I used `minicom -h -D /dev/serial0` on the rpi to verify data was being received from the SKR, assuming it was periodic temperature information.

# Reference

- Teaching Tech 3D Printer Calibration - https://teachingtechyt.github.io/calibration.html

Great reference for initial setup

- AndrewEllis93/Print-Tuning-Guide - https://github.com/AndrewEllis93/Print-Tuning-Guide

Detailed setup for pressure advance and klipper specific elements.


- Older setup guide, still relevant - https://old.reddit.com/r/ender3/comments/ec2i9j/how_to_calibrate_your_printers_esteps_and/

# Archive

Octopi original config in sub-dir `./octopi`

- Raspberry Pi 3B - Klipper & mainsail. Moved to RPI Zero 2 to save a lot of space!



