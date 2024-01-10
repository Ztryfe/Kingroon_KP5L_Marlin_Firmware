# Kingroon_KP5L_Marlin
Kingroon KP5L Marlin Firmware for custom StealthBurner toolhead

Marlin 2.1.x bugfix firmware for Kingroon KP5L version distributed november 2023.

With and without BLTouch, 
16 points manual Mesh bed leveling,
25 pints automated bed leveling,
Linear Advance K: 0.08 (PLA),
Input shaping,
double touch to select,
scroll long filenames,
5 languages,
310x310 bed size,
115200 serial port,
290°C and 350°C (*) hotend.

See the archive Configuration.h and Configuration_adv.h files. 

Changes at wiring for the board:

BLTouch:
Put Z-probe plug to Z-Min endstop. Remove the Z-Min switch from the machine.

Stealthburner Neopixel:
Connect 3 pin cable to the last white socket at the bottom left of the board, next to the 3dTouch pins. 
The pinout is: [Signal - Ground - 5v]

Modify Marlin's files as follows:

Marlin/src/sd/Sd2Card.h:

/**
 * Define SOFTWARE_SPI to use bit-bang SPI
 */
#define SOFTWARE_SPI

Marlin/src/sd/SdFatConfig.h

// Set USE_SOFTWARE_SPI nonzero to ALWAYS use Software SPI.
#define USE_SOFTWARE_SPI 1  
