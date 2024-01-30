# WARNING:

This is not a 'build and install' kind of mod - it relies heavily on the users knowledge of what they are doing to make the prusa printer do what it isnt exactly designed to do (use dual z-probes)!

If you wish to do this mod for yourself I would highly recommend checking out the changes to the firmware and exploring the fusion 360 file provided (along with making any necessary changes to make it work with your own setup - it was designed for custom Z-motor mounts along with the BNBSX extruder).

# CLICKY MOD:

This is the main development branch for the clicky mod for the Prusa MK3 (tested on a modified MK3S+ with an BNBSX extruder). The general premise behind this mod is to make first layer calibration easier through a direct bed measurement device similar to the Voron team's 'Clicky' (hence the name). This is done by the following modifications:

- The (S)PINDA probe holder is replaced with one that includes a limit switch sensor (Omron D2F-01F or similar). The fusion 360 model is included in this repository, though keep in mind that the design was made specifically for the BNBSX extruder which features a removable PINDA clip. At the moment I dont have a mounting option for a stock prusa extruder - the pinda connection would need to be changed and the dock redesigned due to the pinda positioning not being the same between BNBSX and stock prusa MK3S+...

- A single pin cut from 3mm stock (should be highly magnetic - I used mold punching ejector pins with I believe are regular steel)

- A dock that attaches to the right Z motor mount (once again, It would need to be redesigned, I personally used a custom Z-motor mount for use with [stepper motor dampers](https://3dprintingcanada.com/products/rubber-vibration-dampers) ).

- The 2-wire connection from the probe needs to be attached to the (currently empty) Y-axis limit switch connector on the Einsy board (orientation doesnt matter). Its the J14 2-pin connector right above the pinda probe connector. You can check out the [Einsy board schematics](https://github.com/ultimachine/Einsy-Rambo/blob/1.1a/board/Project%20Outputs/Schematic%20Prints_Einsy%20Rambo_1.1a.PDF) if you want to see the full list of pinouts to confirm.

- A custom firmware update (this one) to make use of the y-axis limit switch as a 'clicky' switch along with all the necessary motion changes to allow for Z-calibration and mesh-bed-leveling to make use of the clicky probe.

# Hardware requirements:

I provided links to where I got my parts, though you naturally dont have to order from them exactly (ex: aliexpress for screws & nuts is absolutely fine and much cheaper, plus any wires / switches can probably be replaced with whatever is lying around in your misc. electronics stash).

- a 3d printer to print out the plastic parts.

- 3x [10mm long 2M machine screws](https://www.mcmaster.com/91292A833/) (they are small enough you can get the easier to find 12mm screws and just grind 2mm off)

- 3x [2M hex nuts](https://www.mcmaster.com/90710A020/)

- 1x [16mm (or 20mm) 3M button head screw](https://www.mcmaster.com/92095A111/)

- 2x [2M 4mm setscrews](https://www.mcmaster.com/92015A091/)

- 2x [3M 14mm machine screws](https://www.mcmaster.com/91292A027/)

- 1x [limit switch](https://www.digikey.ca/en/products/detail/omron-electronics-inc-emc-div/D2F-01F/83266) (I used Omron D2F-01F as I had them from fixing my mouse, plus they are 'low actuation force', which probably helps with precision as it results in less possible flex while probing)

- 1x 2-wire cable (I had an extra cable from a filament sensor replacement, so I just took 2 of the 4 cables)

- 1x [female molex connector](https://www.digikey.ca/en/products/detail/molex/0050579402/115029) with the required [pins](https://www.digikey.ca/en/products/detail/molex/0016020086/467788). You dont have to use the special one with a clip if you dont want to - I ordered them in as I needed a bunch of other stuff from digikey, but I am currently running with just regular molex connectors instead without any problems.

- 3mm steel rod (should be magnetic, so stainless steel isnt going to work) cut to 11mm length with both ends sanded flat and one end further ground to a slightly pointed tip (~1.5mm diameter)

- 1x [0.125" x 0.125" (3.2mm x 3.2mm) cylindrical neodymium magnet](https://www.digikey.ca/en/products/detail/radial-magnets-inc/8063/15276815) - I used N40 without any special 'high temperature' resistance which is rated officially for ~80c, but due to its form factor (cylindrical with diameter = height) it should actually be able to handle up to 110c without suffering any permanent strength loss. In either case the plastic chassis will likely fail before the magnet does.

# Assembly:

Should be rather self explanatory:

- Import the STL for the body into your slicer (if you made any modifications in fusion, I would recommend exporting the entire clicky assembly as 1 part in order to allow for better printing)

- Place it face down on its side (with the pinda cutout facing up)

- Scale the stl as necessary to account for shrinking (100.6% is what I used for ASA, though honestly its so minor you can just ignore this)

- Split the stl into multiple objects (not parts!) and move the cover part (the one with the cutouts for the nuts) off to the side. Ideally you want to print it as a vertical wall since it has features on both sides. Prints just fine if you add a brim to it (either through the brim function or just placing a couple cubes of .25mm height and ~15x15mm size on the two sides).

- The 3 objects left behind should be printed as they are - this will make the 'springs' connecting the body to the lever print correctly as a single continuous line.

- The lever needs a support enforcer on the lower part (where the hole for the magnet is). Just make sure you dont accidentally add supports in the magnet hole or (worse) the set screw holes!

- Print however you like (I used ASA as its going to be placed quite close to the build plate), though I recommend 0.15mm layers, 4 perimeters, .4 nozzle.

- Print the dock stl (I used PETG for this, no particular preferences) and clean out the pin dock hole with a 3.1mm to 3.2mm drill. You could also update the model for a larger hole size and not clean it, though I highly recommend using the drill approach as it ensures smooth sides which lead to better reliability during pin deposit operations.

- cut out the plastic on the bottom around the 3M hole (its there to provide better 1st layer adhesion) and use a 3mm drill (or just an exacto knife again) to cut out the 3M hole (sacrificial bridge to make the hole print better)

- Insert the 2 set screws into the side holes for them to the two sides of the magnet hole.

- Insert the magnet as far in as you can. It should poke out of the hole by ~.1mm. At this point try to ensure the magnet is as flat as possible (I personally used a long 3mm rod and held the plastic part against the wall to see any misalignments) 

- Tighten the set screws - keep in mind that the magnet might shift, so check for alignment as in the previous point as you tighten the screws, and in fact you can use the two screws to make the alignment better by selectively loosening one and tightening the other.

- pass the wires through the top hole of the main body and into the inside, solder the wires to the front and back pins of the limit switch (cut off the middle pin). You want the limit switch to be placed with the pin closer to the back (away from the lever and towards the pinda cutout).

- making sure you dont squish the wires place the three M2 bolts through the housing and the limit switch, then cover with the 2nd part and use the 3x nuts to tighten everything. I would recommend putting the M3 bolt through its provided hole to ensure the parts are aligned and then tightening the M2 screws.

- make sure the probe clicks properly! you should be able to press lightly on the lever and hear a click from the switch, with another click as you release the lever. If it gets stuck then you can either try to loosen the M2 screws and 'push' the switch further inwards, or change the model to have a bit more clearance between the switch and the lever. Should be fine though.

- attach the clicky probe and use it to hold the pinda probe in place. As with the pinda probe assembly you want to ensure optimal offset for the pinda probe from the nozzle (I used the [pinda calibration](https://www.printables.com/model/57049-lehre-fur-pindaspinda) print for this). You can pass the wire through the same way as the pinda wiring, though its up to you if you want to do that now or just dangle it loosely from the extruder to the einsy case until you confirm everything works (should help with any re-wiring if necessary if you run into problems).

- Plug the clicky probe into the y-axis limit switch (add the 2 pin molex connector if you havent already)

- Update the firmware

- On the LCD go into support -> sensor info which should have an added value for the CLICKY sensor. If you press up on the clicky lever the sensor should switch from 0 to 1.

- Attach the dock to the right Z-motor mount (14mm M3 screws are used for this)

- Cut the 3mm pin to ~12mm length (11mm is what I used, but its best to cut to 12 and sand it down to 11) and sand down both sides flat. I would recommend printing out a 100mm x 20mm x 10mm (l-w-h) box with a cylindrical cutout ~3 - 3.1mm in diameter that you can use to 'insert' the pin into and hold flat against the desk as you sand the rod as it would ensure the end is perfectly perpendicular.

- Optionally you can grind one of the sides at ~45deg angle to a 1.5mm diameter point. I think it helps decrease heat transfer from the bed to the pin (and magnet) during probing, though tests have shown that it doesnt have much of an effect on precision.

- Place the pin in the dock (it should go in smoothly, and its fine if it isnt perfectly vertical - mine can tilt by around 10 degrees side to side and works without issues as the magnet will help align everything.)

- Optionally run XYZ calibration to confirm the PINDA sensor isnt too high.

- Run Z-calibration (or just wait until the XYZ calibration gets to the Z part with the steel sheet) and carefully watch with your hand on the restart button. Ideally the printer will home z with the pinda probe, then raise up, go to the rightmost position, lower down (picking up the clicky pin), raise back up, go ~30mm left, lower down to confirm the probe pin is in place, raise back up, move to the 0,0 position, start probing the bed (3x3 times), raise back up, go to the dock, lower down to insert the pin into the dock, slowly move leftwards to release the pin, move ~30mm left and go down to confirm the probe pin is no longer attached, raise back up, move to the 0,0 position, lower down to z=0 (ready for printing).

- Run bed mesh calibration (from the calibration menu) - should work pretty much the same as Z-calibration (home xyz if not homed, pick up pin, do MBL, deposit pin, move to 0,0 for printing)

- Run first layer calibration - expect the live-z value to be approximately <pin length> - 9mm (for example I have a 11.00mm pin and use live-z of -2.090mm). This naturally depends greatly on your nozzle!

- I would recommend heat soaking your bed for ~30 min before printing as I found that it takes around that long for the bed to stop deforming. At the very least add a 2-5 min delay after bed temperature is reached in the beginning g-code of your slicer.

# Prusa Firmware MK3

This repository contains the source code and the development versions of the firmware running on the [Original Prusa i3](https://prusa3d.com/) MK3S/MK3/MK2.5S/MK2.5 line of printers.

The latest official builds can be downloaded from [Prusa Drivers](https://www.prusa3d.com/drivers/). Pre-built development releases are also [available here](https://github.com/prusa3d/Prusa-Firmware/releases).

The firmware for the Original Prusa i3 printers is proudly based on [Marlin 1.0.x](https://github.com/MarlinFirmware/Marlin/) by Scott Lahteine (@thinkyhead) et al. and is distributed under the terms of the [GNU GPL 3 license](LICENSE).

This repository contains _development material only!_


# Build
## Linux
There are two ways to build Prusa-Firmware on Linux: using [CMake](#cmake) (recommended for developers) or with [PF-build](#pf-build) which is more user-friendly for casual users.

### CMake
#### Quick-start
The workflow should be pretty straightforward for anyone with development experience. After installing git and a recent version of python 3 all you have to do is:

    # clone the repository
    git clone https://github.com/prusa3d/Prusa-Firmware
    cd Prusa-Firmware

    # automatically setup dependencies
    ./utils/bootstrap.py

    # configure and build
    mkdir build
    cd build
    cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=../cmake/AvrGcc.cmake
    ninja


#### Detailed CMake guide
Building with cmake requires:

- cmake >= 3.22.5
- ninja >= 1.10.2 (optional, but recommended)

Python >= 3.6 is also required with the following modules:

- pyelftools (package `python3-pyelftools`)
- polib (package `python3-polib`)
- regex (package `python3-regex`)

Additionally `gettext` is required for translators.

Assuming a recent Debian/Ubuntu distribution, install the dependencies globally with:

    sudo apt-get install cmake ninja python3-pyelftools python3-polib python3-regex gettext

Prusa-Firmware depends on a pinned version of `avr-gcc` and the external `prusa3dboards` package. These can be setup using `./utils/bootstrap.py`:

    # automatically setup dependencies
    ./utils/bootstrap.py

which will download and unpack them inside the `.dependencies` directory. `./utils/bootstrap.py` will also install `cmake`, `ninja` and the required python packages if missing, although installing those through the system's package manager is usually preferred.

You can then proceed by creating a build directory, configure for AVR and build:

    # configure
    mkdir build
    cd build
    cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=../cmake/AvrGcc.cmake

    # build
    ninja

By default all variants are built. There are several ways to restrict the build for development. During configuration you can set:

- `cmake -DFW_VARIANTS=variant`: comma-separated list of variants to build. This is the file name as present in `Firmware/variants` without the final `.h`.
- `cmake -DMAIN_LANGUAGES=languages`: comma-separated list of ISO language codes to include as main translations.
- `cmake -DCOMMUNITY_LANGUAGES=languages`: comma-separated list of ISO language codes to include as community translations.

When building the following targets are available:

- `ninja ALL_MULTILANG`: build all multi-language targets (default)
- `ninja ALL_ENGLISH`: build all single-language targets
- `ninja ALL_FIRMWARE`: build all single and multi-language targets
- `ninja VARIANT_ENGLISH`: build the single-language version of `VARIANT`
- `ninja VARIANT_MULTILANG`: build the multi-language version of `VARIANT`
- `ninja check_lang`: build and check all language translations
- `ninja check_lang_ISO`: build and check all variants with language `ISO`
- `ninja check_lang_VARIANT`: build and check all languages for `VARIANT`
- `ninja check_lang_VARIANT_ISO`: build and check language `ISO` for `VARIANT`


#### Automated tests
Automated tests are built with cmake by configuring for the current host:

    # clone the repository
    git clone https://github.com/prusa3d/Prusa-Firmware
    cd Prusa-Firmware

    # automatically setup dependencies
    ./utils/bootstrap.py

    # configure and build
    mkdir build
    cd build
    cmake .. -G Ninja
    ninja

    # run the tests
    ctest


### PF-build
PF-build is recommended for users without development experience. Download or clone the repository,
then run PF-build and simply follow the instructions:

    cd Prusa-Firmware
    ./PF-build.sh

PF-build currently assumes a Debian/Ubuntu (or derivative) distribution.


## Windows
### Visual Studio Code (VSCode)
#### Prerequisites

* [Visual Studio Code](https://code.visualstudio.com/)
* [CMake Tools plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
* [Python](https://www.python.org/)
* [Git Bash](https://git-scm.com/downloads)

#### First time setup

Start by cloning the Prusa-Firmware repository

    git clone https://github.com/prusa3d/Prusa-Firmware

Open the `Prusa-Firmware` folder in VScode.

Open a new terminal in VScode (Terminal→New Terminal) and run

    python .\utils\bootstrap.py

This will download all dependencies required to build the firmware. You should see a `.dependencies` folder in the Prusa-Firmware folder.

Reload VScode. If all works correctly you should see the VScode automatically configuring the CMake project for you. If this doesn't happen you likely need to set the CMake kit; This can be done in two ways:

1. Type `Ctrl+Shift+P` and search for `CMake: Select a Kit`. Select `avr-gcc`. If none appear, Scan for kits first.
2. If 1) does not work for some reason, as a last resort you can edit the CMake Tools settings. Search for "Additional Kits" and add `.vscode/cmake-kits.json` to the list.

After updating the kit, you may need to reload VScode.

#### Building

To start building a firmware, click the CMake Tools plugin icon on the far left side. You will get a very large list of targets to build. Find the firmware you'd like to build (like `MK3S_ENGLISH`) and select the small icon which shows "Build" when hovered over.

The built .hex file can then be found in folder `Prusa-Firmware/build`


## Arduino IDE (deprecated)

Using Arduino IDE is still possible, but _no longer supported_. Prusa-Firmware requires a complex multi-step build process that cannot be done automatically with just the IDE. For a long time we provided instructions to use Arduino in combination with shell scripts, however starting with 3.13 the build system has been completely switched to `cmake`.

Building with Arduino IDE results in a *limited* firmware:

- Arduino IDE can only build a single, english-only variant at a time that you manually have to select
- The build will not be reproducible (meaning you will likely get a different binary every time you build the same sources)
- You need to download, patch and select the correct board definitions by hand

For these reasons, you should think twice before reporting issues for a firmware built with Arduino. If you find a bug in the firmware, building and testing using CMake should be your first thought. Issues regarding Arduino builds are answered by the community and are not officially supported.


### Environment preparation

Install "Arduino Software IDE" from the official website https://www.arduino.cc -> Software -> Downloads. Version 1.8.19 or higher is required.

Setup Arduino to install and use the Prusa board definitions:

- Open Arduino and navigate to File -> Preferences -> Settings
- To the text field "Additional Boards Manager URLs" add `https://raw.githubusercontent.com/prusa3d/Arduino_Boards/master/IDE_Board_Manager/package_prusa3d_index.json`
- Open Board manager (Tools -> Board -> Board manager)
- Install "Prusa Research AVR Boards by Prusa Research"


### Source code preparation

Clone or download this repository to your local drive.

In the subdirectory `Firmware/variants/` select the configuration file (.h) corresponding to your printer model and manually copy it to `Firmware/Configuration_prusa.h`

Run "Arduino IDE", then

- Open the file `Firmware/Firmware.ino`
- Select the target board with Tools -> Board -> "PrusaResearch Einsy RAMBo"
- Open `Firmware/config.h` and change `LANG_MODE` to 0.


### Compilation and upload

- Run the compilation: Sketch -> Verify/Compile
- Upload the result code into the connected printer: Sketch -> Upload
