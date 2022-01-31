# klipper_config
Klipper config for Creality Ender 3 V2

Tweaked to suit printer & my needs.

26/Jan/2022 - NOT WORKING - migrating to new SKR board & mainsail

# Hardware
- Creality Ender 3 V2
- CR Touch
- Raspberry Pi 3B - klipper & mainsail
- Hemera Direct Drive
- Dual Z screw after installing heavyweight Hemera
- BTT SKR 2 - klipper
- a vast array of M3 screws, bolts, washers, fans, wire, crimpers, JST/Dupont fittings, heat shrink covers and solder to patch things together.

## Build
2022-01-26
- WIP - migrating to BTT SKR2 & Mainsail (from stock & octopi `./octopi`)

2022-01-??
- Dual Z screw kit via Amazon. Tricky to install and requires some Z-axis stepper cable routing around the back of the PSU as the existing cables are ultimately very short and don't reach. Provided Z-Split cable goes down back of PSU, then joins up to existing cable near mother board.

2022-01-01
- Hemera Direct Drive upgrade
- Noctua 4010+Buck on Hemera after I caught the stock Hemera fan and snapped a blade :'(
- Swapped to Hemera metal backplate from Amazon as the printed one had flex despite ribs & 85% fill. Metal backplate isn't great but it's rigid.
- Provided Hemera thermistor and heat cables are too short when the extruder is at X=max,Y=min,Z=max for a reasonable run into the controller board so had to hack the covers and ultimately bring those cables around the side. Still short but it _just_ works.

Hemera: Printed backplate, fan duct and attachments

2021-12-01
- Replaced all fans with Noctua variants and buck converters to reduce noise. CPU cover, PSU cover, "Briss moto" cooling w/ 2x Noctua 4010 and riser feet

## Hemera install
"Dry fit" all components & parts for complete Hemera install before I did it.
You will need a wide selection of M3 bolts, nuts & washers from 5mm up to 22mm
Be prepared for electronics, wiring, soldering, etc.
Most online guides/videos are made by people with multiple printers so they can print parts if required during the build. If, like most people, you have 1 printer then test everything before you touch your working printer.
I printed various backplates, ducts, connectors, adapters and test fitted them all to the Hemera before I actually dismanteled the printer and rebuilt.

Things of note
- X-end stop hitting various backplates during Hemera required mods to those
- Most backplates are built for BL Touch

### Hemera retraction
Retraction 0.3mm at 45mm retract, 25mm detract. 
BEWARE that if youre detract speed is too high, you get gaps on the model exactly where the "detraction"s are shown in Prusaslicer.

# Software
Started using Cura, moved to Prusaslicer v2.4+ for finer control.
Fusion 360 for STL mods

- Prusaslicer bug where "Gap Speed">0 breaks all Auto Volume speeds. Appears when you try and use Volumetric Speed and no changes occur. https://github.com/prusa3d/PrusaSlicer/issues/6844


# BTT SKR V2
w/ 5 x tmc2209

Board does not fit inside 1 side of the under-carriage so dedicated left & right carriages are required to host it.
The USB-A cable protrudes a long way, so take that into account.

## Stepper End stops
SKR has 3-pin stops where the Stock has 2-pin stops. Inside the 3-pin male, push the 2-pin female in at end away from the steppers. I used side-cutters to strip the tiny outer alignment shims to get a good fit without spraining the board.

## CR Touch
CR Touch wiring, VERY different to BL Touch. Be careful!! Pretty much reversed!!

Split the 5-wire female JST into a 3 & 2. I carefully retracted the pins from the 5-block and pushed them into 2 new blocks as below

### CR touch - reference
https://www.reddit.com/r/BIGTREETECH/comments/pjrkj2/crtouch_wiring_for_btt_skr_v14_and_skr_v2/

https://www.reddit.com/r/Creality/comments/pl4fyv/creality_cr_touch_wiring_diagrampinout/
[ blu | red | yel | blk | wht ]
[  G  |  V  | IN  | G   | OUT ]

Reminder graphic here: https://imgur.com/a/39DU1cv

### Creality board 5-pin JST block
COLOUR	stock board label PIN       SKR
White	G                 GND       GND
Black	V                 +5V       +5V
Yellow	IN                PB0 SIG   PE5
Red 	G                 GND       GND
Blue	OUT               PB1 SIG   PE4

### SKR JST blocks
   3-pin sensor     ~ 2-pin probe
[ wht | blk | yel ] ~ [ red | blu ]
[ GND | +5V | PE5 ] ~ [ GND | PE4 ]


## Steppers
When installing, needs the X stepper direction inverting from stock config by putting a `!` at the start of the klipper config.
`dir_pin: !PE1 ; this is inverted with the "!" from the stock board`
Make sure the config has the appropriate tmc2209 blocks are the distance will be wrong
e.g., `[tmc2209 stepper_x]`

## Raspberry PI
ref: https://www.reddit.com/r/3Dprinting/comments/n73s1j/pi_zero_w_klipper_fluidd_mainsail_guide_skr_mini/
YMMW: Don't use this literally but as a general guide, config changes required.

Connect RPI via GPIO to remove need for massive USB-A cable

(@RPi) GP6  => (@SKR - TFT) GND, 2nd pin from left (steppers at top)
(@RPi) GP10 => (@SKR - TFT) PA9, TFT 3rd pin from left (middle)
(@RPi) GP8  => (@SKR - TFT) PA10, 4th pin from left

My wiring
GP6 - black - pin 2
GP10 - gray - pin 3
GP8 - white - pin 4

https://github.com/bigtreetech/SKR-2/issues/13#issuecomment-831507297

```
On SKR-2 PA9 is TX and PA10 is RX. So pin 10 (RXD0) of RPi would go to the middle pin (PA9) of tft connector on SKR-2 and pin 8 (TXD0)of RPI would go to the 4th pin from left (PA10) on tft connector. And then or course, pick any ground pin on rpi and connect to second pin over from left (GND) on SKR-2.
```


# Archive
Octopi original config in sub-dir `./octopi`