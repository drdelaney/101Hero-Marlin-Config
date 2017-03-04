# 101Hero-Marlin-Config
Marlin 1.1.0rc8 Config files for the 101Hero

Notice
==============
While I did my best to create this, I will warn you that you should use this at your own risk.
The pinouts were mapped by someon other then myself (see thanks below) and I cannot guarantee that they are correct.
Using this config and related Marlin modifications may cause irreparable damage to you or your printer or harm to yourself.

Uploading the board
==============

Arduino Software
--------------
You will need to use the arduino software from https://www.arduino.cc.
This has been tested with 1.6.13, but may work with other 1.6.x or 1.8.x packages.

Addon Software
--------------
Once the Arduino IDE is installed, you will want to add the Sanguino board libraries.
You can review the instructions at [https://dustsreprap.blogspot.com/2015/06/better-way-to-install-sanguino-in.html] (https://dustsreprap.blogspot.com/2015/06/better-way-to-install-sanguino-in.html)

The quick and dirty instructions are
- Start up Arduino IDE
- Open up the menu   File > Preferences 
- Add the following to the "Additional Boards Manager URLs:
  - https://raw.githubusercontent.com/Lauszus/Sanguino/master/package_lauszus_sanguino_index.json
  - If is already something in here, prepend or append the above line, seperating with a comma ",".
- Click OK
- Open the menu Tools > Board > Boards Mananger
- Find or search for Sanguino
- Click Install
- Close the Board Mananger
- You may need to restart the Arduino IDE

**NOTE:** You may need to make a change to a file before restarting the Arduino ISP.  See below for the  stk500_getsync() error.

Selecting the board
--------------
Once the Sanguino board is isntalled, Click on Tools > Board > and select Sanguino (should be at the bottom, might need to scroll down).

Initial upload to the board
--------------
The first upload may need to have a seperate ISP programmer. This can be done with any ISP programmer that can write to ATMEGA chips. (AVR ISP mkII, Arduino as ISP, etc)

I keep getting a stk500_getsync() error!
--------------
You may need to make a change to a file to fix this.
In a windows 7/8/10 environment, this is under your AppData/Local path.
You can open this by clicking on start and typing in %LOCALAPPDATA% followed by <enter>. This will open a window. From here, open the following folders:
Arduino15 > Packages > Sanguino > hardware > avr > 1.0.2. Copy the "boards.txt" to a new file, such as "old_boards.txt".
Edit boards.txt with a text editor which supports UNIX line breaks (VIM/gVIM/Notepad++/WordPad).
Look for a line containing: sanguino.menu.cpu.atmega1284p.upload.speed
and change the value from 115200 or 57600. Save the file, and restart the Arduino IDE. Try the upload again.

Making changes to the confiuration
==============
Feel free to make changes to the configuration as suited for your needs.
Most of the values came from either a stock delta configuration or the original 101Heros configuration, using an attached LCD screen.

I did have to guess on a few settings (below), which may need to be tweaked or changed.

Guessed Settings
--------------
#define TEMP_SENSOR_0 1
#define DELTA_DIAGONAL_ROD 142.5
#define DELTA_SMOOTH_ROD_OFFSET 115.0
#define DELTA_EFFECTOR_OFFSET 23.5
#define DELTA_CARRIAGE_OFFSET 15.0
#define DELTA_PRINTABLE_RADIUS 50.0
#define HOMING_FEEDRATE_Z  (15*60)

Thanks
==============
I would like to mention and thank all the people at user101.com for work on looking at and figuring out some variables for the marlin configuration.
While I measured pretty close to the values they are using, I ended up using the values that workshoptinkerers listed.
Granted I was using these settigns for my RAMPS 1.4 board, they moved over to the 101hero board with no issues.
[This is the forum post that got me in the right direction] (http://101user.com/index.php/topic,126.0.html)

I would also like to thank Gábor Héja from the 101 Hero (Unofficial) facebook group.
Without his help, I would not have been able to take the pin mappings he found and map them to the arduino pins.
[I used this image for the conversion] (http://openhardware.ro/wp-content/uploads/ATmega1284_Arduino_Pinout.jpg)

The mappings he found, with my changes are as follows:
```
D21 - pc5 - x dir
D15 - pd7 - x step
D23 - pc7 - y dir
D22 - pc6 - y step
D2  - pb2 - z dir
D3  - pb3 - z step
D0  - pb0 - e dir
D1  - pb1 - e step
D24/A7 - pa7/adc7 - connector "E" // 100k Thermistor
D7  - pb7 - transistor gate for connector "G" // Extruder 0
D18 - pc2 - x end stop
D19 - pc3 - y end stop
D20 - pc4 - z end stop
```

And finally, I would like to thank the 101hero team for making this cheap 3D printer that enabled a large number of people to get togeather and hack the crap out of it to make it better!
