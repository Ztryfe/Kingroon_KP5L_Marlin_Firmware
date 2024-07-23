# Kingroon KP5L With StealthBurner Toolhead
Kingroon KP5L Marlin Firmware for custom StealthBurner Toolhead

Marlin 2.1.x bugfix firmware for Kingroon KP5L version distributed november 2023.

With BLTouch offset to match this carriage & bltouch mount:
https://www.printables.com/model/428517-kp5l_carriage_sb


10x10 points Unified Bed Leveling

Linear Advance K: 0.08 (PLA)

Input shaping & menu enabled

Double touch to select & scroll long filenames.

310x320 bed size, extend X axis for an eventual nozzle cleanner.

115200 serial port, HOST COMMANDS enabled

300C hotend using a ceramic ring heather and this Thermristor:

100kΩ ATC Semitec 104GT-2/104NT-4-R025H42G - Used in ParCan, J-Head, and E3D, SliceEngineering 300°C 


# Wiring changes needed

BLTouch:
Put Bltouch 2 pin plug to Z-Min endstop. 
Remove the Z-Min switch from the machine.

# Stealthburner Neopixels on Marlin and KP3S v1.3 Board

Neopixels cannot bet setup without incurring in severe performance penalties due the use of software driven SPI.

Here is how to set it up if you want to try ( or to eventually use Klipper)
Use this kit:
https://www.fysetc.com/products/fysetc-voron-stealthburner-led-kit-neopixel-rgbw-mini-button-pcb-leds-ptfe-wiring-harness-for-voron2-4-trident-3d-printer-parts

Connect 3 pin cable to the last white socket at the bottom left of the board, next to the 3dTouch pins. 
The pinout is: [Signal - Ground - 5v]
This is "PB2" Port.

To enable SOFTWARE_SPI for the SD Card:

Modify Marlin's files as follows:

Marlin/src/sd/Sd2Card.h:

/**
 * Define SOFTWARE_SPI to use bit-bang SPI
 */
#define SOFTWARE_SPI

Marlin/src/sd/SdFatConfig.h

// Set USE_SOFTWARE_SPI nonzero to ALWAYS use Software SPI.
#define USE_SOFTWARE_SPI 1  

Otherwise you will run into a bug with SD Card access & Neopixels with the Kingroon KP3S Board inside the KP5L.
http://github.com/MarlinFirmware/Marlin/issues/25328

Finally, at Configuration.h, uncomment this:

// #define NEOPIXEL_LED

At the time of this change this made the cpu not being able to keep up on circles / curves.
Trying both SD Card and Neopixel enabled with regular DMA also caused hicups ( but was able to read SD Card)
