# Firmware

## To Simply Verify Function

It is possible to verify functionality without building using [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases).

![Imgur](https://i.imgur.com/75BHCKI.png)

1. Verify that an atmega32u4 is detected
2. Download any of the firmwares below which suits the options selected, and open it in QMK Toolbox


- No options: [helix_rev2_default.hex](http://qmk.fm/compiled/helix_rev2_default.hex)
- 5-row OLED and backlight: [helix_rev2_default_oled_backlight.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_oled_backlight.hex)
- 5-row OLED and underglow: [helix_rev2_default_oled_underglow.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_oled_underglow.hex)
- 4-row OLED and backlight: [helix_rev2_default_4rows_oled_backlight.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_4rows_oled_backlight.hex)
- 4-row OLED and underglow: [helix_rev2_default_4rows_oled_underglow.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_4rows_oled_underglow.hex)
-
![Imgur](https://i.imgur.com/hLygSgB.png)

1. Press the reset button on helix, and verify that it shows as "connected"
2. Immediately press flash

![Imgur](https://i.imgur.com/dH2Wser.png)

If a message similar to this appears, flashing has succeeded.

Please verify that typing is possible using these firmwares.

To change the layout, use the build guide below.


## Setting up the build environment

Create the build environment according to the official guide of QMK.

https://docs.qmk.fm/#/newbs_getting_started

## Build and flash

Run the following at the root directory of the QMK folder:

    make helix:default

To flash at the same time, attach `:avrdude` to the command:

    make helix:default:avrdude

For flashing via GUI, use [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases) as described earlier.

Both halves must be flashed.

## Customize

Copy and rename the `default` folder in `/keyboards/helix/rev2/keymaps/`.
This new folder will be used from now on.

For building this new keymap, the following command will be used:

    make helix:<new keymap folder name>

## Editing the keymaps

The default keymap is stored in keymap.c. It can be edited to modify the keymap freely.

Please see [this page](https://docs.qmk.fm/#/keycodes) for a keycode reference.

![Imgur](https://i.imgur.com/YxZT1TL.png)

## Making the keymap 4 rows

Within the folder, change the field HELIX_ROWS rules.mk from 5 to 4.

    HELIX_ROWS = 4

## Enable RGB backlighting

In the same file, change the LED_BACK_ENABLE from no to yes.

    LED_BACK_ENABLE = yes

##  Enable RGB underglow

Again in the same file, change LED_UNDERGLOW_ENABLE from no to yes.

    LED_UNDERGLOW_ENABLE = yes

## Enable OLED display

Again in the same file, change OLED_ENABLE from no to yes.

    OLED_ENABLE = yes


### Edit font data
The font data is stored in helix/common/glcdfont.c.
This data can be edited in the following ways for modifying OLED content.

#### Using the web tool

The web tool created by [@teri_yakichan](https://twitter.com/teri_yakichan) can be used to modify the file easily.

[Helix Font Editor](https://helixfonteditor.netlify.com/)

#### Using an image editor

To use an image editor, do the following to convert text to image.

1. Take the image data from glcdfont.c and move it to a text file.
0x00, 0x00 ... 0x00
2. Use the script to convert to image
3. Edit the image
4. Use the script to convert back to text
5. Insert to glcdfont.c

An example image being edited:

![Font](https://i.imgur.com/adJX6CX.png)

The following script is used for conversion.
https://github.com/MakotoKurauchi/helix/tree/master/FontConverter

Converting text to image

    $ python3 hex2img.py inHex.txt outImage

Converting image to text

    $ python3 img2hex.py inImage.bmp > outHex.txt

### Creating a font data specific to the keymap

Editing helix/common/glcdfont.c affects all keymaps. To make a font data unique to a keymap, edit the LOCAL_GLCDFONT field in rules.mk:

    LOCAL_GLCDFONT = yes

Then, rename glcdfont.c to helixfont.h and place it in the same directory as keymap.c.



## Other customization

QMK has many features. See the [docs](https://docs.qmk.fm) and others' customizations to build your own unique helix.
