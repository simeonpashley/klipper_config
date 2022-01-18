# klipper_config
Klipper config for Creality Ender 3 V2

Tweaked to suit printer & my needs.

# Hardware
- Creality Ender 3 V2
- CR Touch
- Hemera Direct Drive
- a vast array of M3 screws, bolts, washers, fans, wire, crimpers, JST/Dupont fittings, heat shrink covers and solder to patch things together.

## Build
TODO:
- Dual Z screw after installing heavyweight Hemera

2022-01-01
- Hemera Direct Drive upgrade
- Noctua 4010+Buck on Hemera after I caught the stock Hemera fan and snapped a blade :'(

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
