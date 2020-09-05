# Floppy emulator with OSD
This is a fusion of a "Gotek" and a "Bluepill" that can provide both FlashFloppy and FF_OSD on a single board. Thank you to Keir Fraser for his firmware https://github.com/keirf/FlashFloppy, and to the chinese people for the original device.

Thanks to the OSD and Amiga keyboard support, LCD/oled display or buttons are no longer necessary and the device can be almost completely hidden inside Amiga computers. It is still possible to install a display and buttons, though.

This board also has something special : when connected to an "Amiga dual floppy selector" board, it can daisy-chain to the original floppy drive, and the OSD let you choose dynamically which drive is DF0 and DF1. Thanks to this you can enjoy both your original games on floppies and disk images on USB or SDcard !

# Disclaimer
This is a hobbyist project, it comes with no warranty and no support. Also remember that the Amiga machines are about 30 years old and may fail because of such hardware expansions.

This version is not endorsed by the author of FlashFloppy, please don't bother him with issues you might have because of it.

I publish my work under the CC-BY-NC-SA license. My modifications to the FF_OSD source are under "the unlicense", like the original code.

If you find it useful and want to reward me : I am always looking for Amiga/Amstrad CPC hardware to repair and hack, please contact me.

# BOM
- 1x STM32F105RBT6
- 1x STM32F103C8T6
- 1x 74LS07D
- 1x SPX3819M5-L-3-3 3.3v LDO
- 2x 8MHz HC-49 crystals
- 3x 10uF 0805 capacitors
- 9x 100nF 0805 capacitors
- 4x 22pf 0805 capacitors
- 2x 1k 4x0603 resistor arrays
- 2x 22 ohm 0805 resistors
- 3x 4k7 0805 resistors
- optional for activity LED : 1x 0805 resistor and LED
- 1x 2x17 pins header. Remove pin 3 which is a key.
- optional for drive daisy-chain : 1x 2x17 pins socket. Remove pin 3 which is a key.
- 1x USB A Female Socket, type G54
- 1x vertical floppy power connector or 1x4 pin header
- a jumper or wire for DS0/DS1 selection
- pin headers or wires for keyboard, video, drive selection, piezo transducer, SD-card, buttons, rotary encoder, display

# Making it
Components are SMD, and have quite thin pin pitch. You need to know what you are doing.

You may choose to install the USB and/or SD connector on a remote board, to make them accessible through trapdoors or openings in the case. You may solder buttons, rotary encoder, LED, display and piezo transducer.

Check for shorts at least between 5V, 12V and GND traces before applying power !

The programming port do not need to be soldered since it needs to be programmed just once : you can just hold it in place during the few seconds required for programming.

If you plan to use the "Amiga dual floppy selector", then you need to compile FF\_OSD from source, with the small modifications proposed in this repository. Use `patch -ru -d FF_OSD-master  < patch` to apply them. Otherwise you can use stock firmware. FlashFloppy does not require any modification.

To program the F103 uC then the F105 uC, I personally use a STLINK clone dongle with the stlink tool : https://github.com/stlink-org/stlink

To connect the wires to components on the A500 motherboard, here is a tip :
- Take a metal pin from the female 2.54mm pin socket, which is shaped as a lyre. The one you removed from pin 3 for example.
- Solder the wire on the pin, where you normally solder it.
- Place the pin, the solder joint and the end of the wire inside heat-shrink tube, with only 1mm of metal uncovered from the tips of the lyre.
- Snap the tip on the lyre on the component where you want to connect.

# Using it
- Connect the device to the floppy ribbon and power plug.
- Connect CSYNC, KB_CLOCK and KB_DATA to the motherboard as explained in FF_OSD wiki.
- connect VIDEO to the motherboard THROUGH A 270 OHM RESISTOR ! I know I should have added this to the board.
- If you choose to use a second drive and the "Amiga dual floppy selector", connect A and B signals of both devices, connect the second drive to the back of the device or to the end of the special 3-connector ribbon cable. Don't forget the 2nd drive power.
- Insert the USB thumb drive or SD-card
- Turn on the Amiga, enjoy.

To change the drives configuration using the "Amiga dual floppy selector" :
- First eject all floppies to prevent confusion of the OS.
- Go to the FF_OSD config menu, change the Drive config setting accordingly.
- If you changed from one to two or two to one drive, then you need to reboot for the second drive to be identified or ignored correctly.

