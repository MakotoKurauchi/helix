# Usage Guide

The usage of Helix is described using the default keymap.

## Connection between the halves

Either a TRS or TRRS 3.5mm aux cable is used.  
(Even with LEDs or OLEDs, a TRS cable works fine.)

* To avoid damage, always connect the aux cable __first__ and USB cable after the halves are connected.

![Imgur](https://i.imgur.com/1alxKG2.jpg)


## Layers

The Helix obviously does not have enough keys compared to a typical keyboard.  
The keymap has multiple layers, moving extra keys to different layers.

|Priority|Layer ID|Layer Name|Contents|
| ---- | ---- | --- | --- |
|High|5|Adjust|Function Keys|
||4|Raise|Symbols (Pink)|
||3|Lower|Symbols (Blue)|
||2|Dvorak|Dvorak layout|
||1|Colemak|Colemak layout|
|Low|0|Qwerty|Qwerty layout (Base)|


Usually hidden, the layers above the base layer appear by using the layer adjust keys. Wherever keys overlap, the keys with higher priority replace the keys below it.

For example, here is an example of "Raise" and "Lower" overlaid above the base.
For example, holding the pink raiser key when pressing `a` registers the F1 key.

![Imgur](https://i.imgur.com/10R4O2P.jpg)

Next, here is the adjust layer overlaid onto base.  
For example, pressing `q` while holding Adjust sends the reset keycode, making the keyboard enter its bootloader (Same as pressing the reset button).

![Imgur](https://i.imgur.com/jaYTsNM.png)

On the default keymap, pressing Raise and Lower together registers Adjust.


## LED Control

To control the LED backlighting and underglow, the keys on the adjust layer are used.

|Command|Default Layout|Keycode|
| ---- | ---- | --- |
|On/Off|Adjust + ,|RGB_TOG|
|Mode|Adjust + Left|RGB_SMOD|
|Reset|Adjust + w|RGBRST|
|Hue Increase|Adjust + .|RGB_HUI|
|Hue Decrease|Adjust + Down|RGB_HUD|
|Saturation Increase|Adjust + /|RGB_SAI|
|Saturation Decrease|Adjust + Up|RGB_SAD|
|Value Increase|Adjust + Enter|RGB_VAI|
|Value Decrease|Adjust + Right|RGB_VAD|

## Switching between Mac and Windows mode

In Mac mode, the EISU and Kana keys function as English/Numerics and Kana input keys respectively.

In Windows mode, the EISU and Kana keys both function as Alt + ` (Japanese IME switcher).
Also, <font color="Red">the Alt and GUI keys are swapped.</font>。

The current mode is displayed on the OLED display.

|Command|Default Layout|Keycode|
| ---- | ---- | --- |
|Mac Mode|Adjust + g|AG_NORM|
|Windows Mode|Adjust + h|AG_SWAP|
