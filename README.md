# rainboard

An open-source isomorphic MIDI controller.

#### Installation of the Rainboard fIrmware:

The Rainboard firmware runs on an Arduino Mega which has two processors on board. The main processor being the ATmega2560, and an ATmega16U2 used as a USB to serial tranceiver. The 16U2 processes USB data from the host PC into serial data and feeds it to the serial communications port on the 2560. This is how the host PC communicates with the Arduino Mega for programming, debugging, and other uses, in this case USB MIDI communication.

(Some Arduino Mega clones use a different chip other than the 16U2 for USB, these will not work on the Rainboard. Please verify your Mega has a 16U2, it will be the chip closest to the USB connector.)



#### The Rainboard firmware consists of two files:

1. rainboard_firmware.ino   - the main Arduino sketch.
2. rainboard16u2.hex   - the USB to serial tranceiver code.



#### Installing the Rainboard firmware consists of two steps:

1. Flashing the ATmega16U2 with the rainboard16U2.hex file.
2. Uploading the compiled rainboard_firmware.ino sketch to the Arduino Mega.



#### To flash the ATmega16U2 with the rainboard16U2.hex file:

This can be accomplished with a DFU Programmer. Follow the instructions for your programmer.

Alternatively, if you don't have a DFU Programmer you can use Atmel FLIP software on a Windows Computer.

1. Go to http://www.atmel.com/tools/FLIP.aspx and download FLIP.
2. Install FLIP. Follow the installation wizard.
3. Disconnect Arduino from USB.
4. Jumper pins 5 and 6 on 16U2 ICSP header (as shown in fig.1). This will keep the 16U2 in RESET.
5. Connect Arduino to USB.
6. Remove the jumper from pins 5 and 6. At this moment, 16U2 goes into DFU mode. A new USB device should be recognized.
7. If driver is not installed automatically, install it from “c:\Program Files\AtmelFlip 3.4.7\usb\”
8. Go to Device manager (Win+Pause -> (Hardware) -> Device Manager) and check if you can see the driver installed correctly. It will be located under Atmel USB Devices -> ATmega16U2.
9. Disconnect Arduino from USB. Jumper pins 5 and 6.
10. Connect Arduino to USB.
11. Remove the jumper from pins 5 and 6.
12. Start FLIP Software: Go to Start -> All Programs -> Flip -> Flip.
13. Go to Settings -> Communication -> USB.
14. Press “Open”.
15. Go to File -> Load HEX file and select the rainboard16U2.hex file.
16.  Press “Run”. This will program the 16U2 with the rainboard16U2.hex file.
17. Now close FLIP, disconnect and reconnect the Arduino, it should be recognized as a MIDI  device named Rainboard.



#### To upload rainboard_firmware.ino to the Arduino Mega:

The most straightforward way to do this is through the Arduino IDE. Make sure you have the proper drivers installed and that you can program the Mega from the Arduino IDE. You will also need two Arduino libraries installed that the Rainboard firmware depends on:

Adafruit-MCP23017-Arduino-Library - https://github.com/adafruit/Adafruit-MCP23017-Arduino-Library

MIDI_Library-5.0.2 -  https://github.com/FortySevenEffects/arduino_midi_library

Make sure your Arduino environment is working, you have the two libraries installed and you can successfully compile the rainboard_firmware.ino sketch.  Also make sure you have already flashed the ATmega16U2 with the rainboard16U2.hex file per the previous step.

1. Power down the Arduino. (unplug from host Computer)
2. Connect a jumper across pins 4 and 6 on the ICSP Header of the 16U2 (as shown in fig.1).
3. Reconnect the Arduino to the host Computer. It should appear as a COM Port Device in the Arduino IDE.
4. Now you can compile and upload the rainboard_firmware.ino sketch to the Arduino in the standard way.
5. After programming, power down (unplug from host Computer), remove the jumper from pins 4 and 6 on the   ICSP Header of the 16U2 (as shown in fig.1). The Arduino should now be fully programmed and ready to mate to the Rainboard. 
6. **Be very careful that all the pins are aligned and inserted properly before fully mating!**
7. Once the Arduino is mated to the Rainboard, reconnect it to the host PC and it should appear as a MIDI Device with the name Rainboard.

![alt text](https://github.com/famulus/rainboard/blob/master/images/Mega-Jumpers.png?raw=true)

