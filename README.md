# rp2040_MCP4725_Sonicator
An implementation of a Raspberry Pi RP2040 Pico and an Adafruit MCP4725 DAC to serially control a QSonica125 sonicator board and tool.

This repository contains the necessary files to set up a Pico microcontroller to serially control a QSonica Sonicator PCB board and Tool.
You can find an implementation of this in the following [repository](https://github.com/machineagency/science_jubilee), as well as its original implementation using a Raspberry Pi SBC and a PCB board [here] (https://github.com/machineagency/sonication_station).

# Setting up the RP2040 Pico microcontroller

The projects implements the [Raspberry Pi Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf). 

To start, you should clone the GitHub repository for the [Pico-sdk](https://github.com/raspberrypi/pico-sdk) in your *PROJECT_DIRECTORY* and set up all the required submodules by running the following command in the sdk directory:

`git submodule update --init --recursive`

You can now follow the instructions to *Quick-start your own project*. 

The `CMakelists.txt`, as well as the `main.c` files can be found here and should be placed in your *PROJECT_DIRECTORY* too.

## Compile the Firmware
Create a `/build` directory and navigate to it, then run the following commands:

`cmake ..`

This creates all the files required to later create the executable `.uf2` files. You can do so by running :

`make`

## Upload the Firmware onto the RP2040
Load the Pico in BOOTSEL mode and plug it into your computer's usb. Now, you can drag-and-drop the generated `.uf2` file into the mass storage device representing the Pico. It should now be automatically ejected and ready to use.

## Editing the Firmware
You can edit the `main.c` file to change which pins you are using to connect to the MCP4725 DAC or which GPIO pin turns on/off the sonicator. 
If you do so, you will need to re-run the following command:

`make`

    Note: if you make changes to the `CMakeLists.txt` file, you will need to re-create the `/build` folder, navigate to it, and run `cmake ..` , followed by `make` too. 

## Hardware Checklist

### Sonicator Tool
* Q125 Sonicator Horn
* Sonicator Probe (various probe sizes, including pn: 4423, pn: 4422, and pn: 4435)
* Sonicator Control PCB, pn: KITVC1025 (20kHz) or pn: KITVC1045 (40kHz)
* Sonicator Wiring Harness
    * 1x [Molex: 0022552102](https://www.digikey.com/en/products/detail/molex/0022552102/303176)
    * 3x [Molex: 0016020086](https://www.digikey.com/en/products/detail/molex/0016020086/467788)
    * 1x [McMaster-Carr: 7243K117](https://www.mcmaster.com/7243K117/) for the sonicator horn wiring
    * 1x [McMaster-Carr: 7243K122](https://www.mcmaster.com/7243K122/) for the sonicator horn wiring
    * 1x [Digikey: ED10562-ND](https://www.digikey.com/en/products/detail/on-shore-technology-inc/OSTVN03A150/1588863?s=N4IgTCBcDaIKIBECMAGArANjAWgHIJAF0BfIA)

### Raspberry Pi Pico Microcontroller
One of the ways to interface with the sonicator control PCB board is using a Raspberry Pi Pico microcontroller. This solution allows the user to interface the tool through their computer directly, instead of relying on a Raspberry Pi SBC. To set up the RP2040 pico, the instructions and necessary files can be found in the `rp2040` folder. 

For this solution, the following items are required:
* 1x [Raspberry Pi Pico RP2040 microcontroller](https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html)
* 1x [Adafruit MCP4725 12-bit DAC](https://www.adafruit.com/product/935)
* 1x [Half-size Breadboard](https://www.adafruit.com/product/64), alternatively you can also purchase a [Half-size soldering breadboard](https://www.digikey.com/en/products/detail/sparkfun-electronics/PRT-12070/5230951)
* 1x [Breadboard wire bundle](https://www.adafruit.com/product/153)
* 1x [2N7000 MOSFET](https://www.digikey.com/en/products/detail/onsemi/2N7000/244278) 
* 1x [100𝜇F Capacitor](https://www.amazon.com/100uF-105%C2%B0C-Aluminum-Electrolytic-Capacitor/dp/B07D6WDQMV/ref=sr_1_3?keywords=100+mfd+capacitor&qid=1705604871&sr=8-3)
* 1x [4.7kΩ Resistor](https://www.adafruit.com/product/2783)

Below is a schematics for the assembly: 
<img src="[https://github.com/MariaPoliti/rp2040_MCP4725_Sonicator/docs/](https://github.com/MariaPoliti/rp2040_MCP4725_Sonicator/blob/main/docs/RaspberryPi_Pico_Microcontroller_Schematics.png)">

