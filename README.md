PiforceTools
============

Piforce Tools drives a Raspberry Pi with Adafruit LCD Plate and interfaces with debugmode's triforce tools to load a NetDIMM board with binaries for a Triforce, Naomi, or Chihiro arcade system.  
it is working with the adafruit LCD module 16x2 LCD Plate - http://learn.adafruit.com/adafruit-16x2-character-lcd-plus-keypad-for-raspberry-pi, and chinese clone from DX http://www.dx.com/fr/p/rgb-negative-16-x-2-lcd-keypad-kit-for-raspberry-pi-black-297384#.Vw-fkHWLTRZ but you need to modify the file Adafruit_CharLCDPlate.py, at line 99 like this 
Code:

~~~~~~
0b00011111, # IODIRA R+G LEDs=outputs, buttons=inputs
~~~~~~
## Enhanced clone of Piforcetools from Amosso75
https://github.com/amosso75/piforcetools
The release from Amosso75 added : 

- Sorts games by arcade system (Naomi 1, Naomi 2, Chihiro, Triforce) ;
- Sorts games by genre (Fighting, Horizontal Shmup, Puzzle, ...) ;
- Enables you to go to the previous/next letter inside any game list ;
- Multi-language support (for now only French & English) ;
- Enables you to give a nickname to each IP address for easy reading
(useful when you have a multi-system setup) ;
- Enables you to define for each arcade system which IP addresses you
allow as a target for uploading. The first IP of this list is the
default one with fast access to upload a game ;
- Enables you to customize the items you want in the main menu and
their order of appearance ;
- Enables you to customize the items you want in the "Games by genre"
and "Games by system" menus and their order of appearance ;
- Easy configuration of inputs (default one is the one I use but I
wrote another one in comments just as an example) ;
- Inputs management recognizes a long button press ;
- Shows a list of the "non matching" .bin files in the roms folder and
enables you to choose an "orphan" game for automatic .bin file renaming
;
- Enables you inside any game list to add or remove a favorite game
(this list is saved in a text file) ;
- A little heart is placed next to a favorite game's name on any list
- Shows a list of your favorite games ;

This version add the RGB led management during the use of the script, a tempo will turn off the backlight of the screen after 15s (by default, easily modified by associated variable in the config.py file). A Shutdown menu has been added too, to halt safely the Rasberry Pi.

It is configured for the Banggood clone of the Adafruit LCDPlate clone 16x2. 

## Banggood clone
For this LCDPlate clone 16x2_LCD_with_Keypad_and_Backlit_SKU:297384  you need to use the patched version od the Adafruit code : http://www.raspberrypiwiki.com/index.php/16x2_LCD_with_Keypad_and_Backlit_SKU:297384 and the archive http://www.raspberrypiwiki.com/index.php/File:16x2LCD-Adafruit-Raspberry-Pi-Python-Code.zip

When plugging the LCD plate on the Raspberry Pi you need to take care that the board does not touch or lay on the metallic cage of the usb connector or RJ 45 connector. If there is a contact, the i2c mcp module is not recognised anymore by the system and the module fails to work. I think a ground appears from the plate board to the pi board preventing the i2c to work.

## Usage

Left/Right buttons allows to select the item in the top view menu : Games by systems, by type, Favorites (need a files to describe favorite games), All games, Ping netdimm and shutdown.  Up/Down navigate items within each mode.  A short press on the Select button will select the item being displayed. A long press on the Select Button will take you in the upper level of the menu.

## Getting Started

You will need the following items to use Piforce Tools:

1. A Raspberry Pi - http://www.raspberrypi.org/ 
2. An SD Card (Minimum 4GB, but I recommend at 8GB or higher)
3. An assembled Adafruit 16x2 LCD Plate - http://learn.adafruit.com/adafruit-16x2-character-lcd-plus-keypad-for-raspberry-pi
4. A Naomi, Triforce, or Chihiro arcade system.
5. A Netdimm with a zero-key security PIC installed.  I cannot provide links for this, but a modicum of Google-fu will get you what you need.  The netdimm will need to be configured in static mode with an IP address of 192.168.1.2, netmask of 255.255.255.0, and gateway of 192.168.1.1.
6. A crossover cable

## Installation

Now you are finally ready to install Piforce Tools.

1. Downlad the piforce tools SD card image: http://downloads.travistyoj.com/piforcetools.img.zip
2. Extract .img file, and use imager tool to write it to your SD card.  If you are using Windows, look for Win32DiskImager.  If you are using Linux or Mac OS, you will use the command line tool dd.  Imaging an SD card is easy, but here is some more information - http://elinux.org/ArchLinux_Install_Guide
3. Use a partition manager tool like Partition Wizard to move the Ext4 partition to the end of the card, and resize the FAT partition to use all unallocated space: http://www.partitionwizard.com/free-partition-manager.html
4. Load up ROMs in the "roms" directory.

## Troubleshooting
I provide this script and image without warranty, and its not feasible to provide support to everyone, but I want to at least provide some troubleshooting steps 

* **LCD powers on, but no text is displayed.** Make sure you adjust the contrast of the LCD Plate.  
* **LCD does not power on** This could be several different things.  First make sure the LCD Plate is assembled correctly by following the usage instructions on Adafruit's product page.  Run the python script provided there and confirm the LCD Plate works.  Double check your solder work.  Depending on your revision of your Raspberry Pi, you may need to change any lines of the Piforce Tools script to specify the bus number when instantiating the LCD Plate object.  For example, change lcd = Adafruit_CharLCDPlate() to lcd = Adafruit_CharLCDPlate(busnum = 0) for a Rev 1 Pi.
* **NO GAMES FOUND! message is displayed** Make sure your roms are in the /home/pi/roms directory and that the filenames match those specified in the piforcetools.py script. 
* **I keep getting Connect Failed! when I try to send a game** Make sure your target device has been configured to be at 192.168.1.2.

## Credit

This could not be done without debugmode's triforce tools script.  All the heavy lifting was done by him, I just made an easy to use interface for his work.  Also shoutout to darksoft for his killer Atomiswave conversions.
