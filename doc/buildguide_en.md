# Build Guide

![picot5400_gallery_00](/images/gallery_00.jpg)

This is a build guide for picot5400.  

picot5400 is a micro controller (RP2040) and trackball sensor (PMW3360) module for mechanical keyboard.  
When building a keyboard with picot5400, please refer to this page for the assembly. Please refer to each keyboard's build guide for all other steps.

## BOM

|Parts|No.|Notes|
|---|---|---|
|picot5400 PCB|1||
|Sensor (PMW3360)|1||
|M2 Spacer 3.5mm|4||
|M2 Screw 5mm|8||
|Bearing Roller|3||
|Stainless Pin (R=2mm, L=6mm)|3||
|Silicone Tube (ID:2mm, OD:3mm)|1||
|Magnet (R=2mm, D=2mm)|8||
|3D Printed Ball Case (Base + Cover)|1||

## Assembly
### picot5400

  First, connect picot5400 to the USB and check if it is correctly recognized by the PC  
  ***This process must be done before soldering. Please note that if the operation cannot be confirmed after soldering, it is not included in the initial defects.***  

  After confirming that the device is recognized as a USB device, install the mouse sensor. Install the mouse sensor on the board from the backside in the orientation shown in the image, and solder from the top surface. Make sure to align the ● mark on the silk with the ● mark on the board.   
  ![picot5400_bg_pmw3360_1](/images/build/bg_pmw3360_1.jpg)

  With the sensor legs firmly in place, secure them with masking tape so that they do not float. Solder 16 legs from the top side. ***Soldering must be done wiht the USB cable disconnected.***  
  Remove the tape attached on the sensor and attached the lens from the top.    
  ![picot5400_bg_pmw3360_2](/images/build/bg_pmw3360_2.jpg)

  ![picot5400_bg_pmw3360_3](/images/build/bg_pmw3360_3.jpg)

  Once the lens is attached, connect it to the USB again and confirm that the cursor moves by moving your hand over the top of the lens.

  After confirming that the sensor is working correctly, apply a soldering iron slightly to the protrusion of the lens from the back side to melt and fix the lens.
  ![picot5400_bg_pmw3360_4](/images/build/bg_pmw3360_4.jpg)  

### Ball Case

　Cut three pieces of the thinner silicone tubes about 3mm long. They can be easily cut with scissors, but be careful to keep the cut surfaces as flat as possible.  
  ![picot5400_bg_ballcase_1](/images/build/bg_ballcase_1.jpg)  

  Pass stainless pins through cut-out silicone tubes.  
  ![picot5400_bg_ballcase_2](/images/build/bg_ballcase_2.jpg)  

  Pass the bearing rollers through the outside of the silicone tubes and adjust them so that they are centered on the pins.  
  ![picot5400_bg_ballcase_3](/images/build/bg_ballcase_3.jpg)  

  Attach the pins with bearing rollers to the three pedestals of the ball case base. Push them in from directly above until you hear them click into place. If the pins do not stick out from the base, it should be ok.
  ![picot5400_bg_ballcase_4](/images/build/bg_ballcase_4.jpg)  

  Fix the spacers in the four corner below ball case base.  
  ![picot5400_bg_ballcase_5](/images/build/bg_ballcase_5.jpg)  

  Put ball case base above picot5400. Put them above a case or a bottom plate depending on keyboards, fix them with screws from the bottom side. Please refer to the build guide of each keyboard for more information.  
  ![picot5400_bg_ballcase_6](/images/build/bg_ballcase_6.jpg)  

## Firmware

  If you wish to write your own firmware, please follow the instructions below.

  - Press the RESET button while holding down the BOOT button on the picot5400 to enter boot loader mode.
  - The firmware is written by dragging and dropping the [.uf2](https://github.com/aki27kbd/picot5400/blob/main/firmware/aki27_picot5400_vial.uf2)file into the drive named RPI-RP2.  　

  Keymap is editable from [vial](https://vial.rocks/).  
  You can confirm that keys and trackball are working correctly with this firmware.

  The default firmware enables "Auto Mouse Layer", with which you can automatically jump into a specific mouse layer when you move trackball. You can toggle on/off this function with the custom keycode `AM_TOG`.

  The source code is available [here](https://github.com/aki27kbd/vial-qmk/tree/vial/keyboards/aki27/picot5400).


## Custom Keycodes

  Several custom key codes can be set for trackball operation.

  Keycode   |Description
  ---------|-----------
  `CPI_SW`  |Change the CPI of the trackball. With the default firmware, each press changes the CPI in the following order: 200 -> 400 -> 800 -> 1600 -> 3200 -> 200....
  `SCRL_SW` |Changes the sensitivity of the sensor in scroll mode. The higher the value, the smaller the amount of scrolling.
  `ROT_R15` |Turns the Y axis of the mouse sensor 15 degrees clockwise.
  `ROT_L15` |Rotate the Y axis of the mouse sensor 15 degrees counterclockwise.
  `SCRL_MO` |	Enables scroll mode for as long as it is pressed.
  `SCRL_TO` |Toggles between scroll mode and mouse mode each time it is pressed.
  `SCRL_IN` |Inverts the scroll direction.
  `AM_TOG` |Toggle the function of auto mouse layer.

  Custom key codes can be set in vial using the custom key code under the User tab.  
  ![CustomKeycode_rev](/images/build/bg_customkeycode.jpg)



## Notes
If you have any problems, please contact us at[Twitter](https://twitter.com/aki27kbd).

The hashtag is #picot5400.
