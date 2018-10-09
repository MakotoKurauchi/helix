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

## To Customize
Download QMK Firmware from the following:

https://github.com/qmk/qmk_firmware/

(Press the green "Clone or download" button, and then "Download ZIP" to obtain a ZIP file.)

Extract after download.

If familiar with git, a `git clone` may be more suitable.

## Setting up the build environment
### macOS
 [homebrew](https://brew.sh) will be used in this guide.
1. Launch terminal
1. Install [homebrew](https://brew.sh) if not installed yet.
1. Run the following commands:

```
brew tap osx-cross/avr
brew tap PX4/homebrew-px4
brew update
brew install avr-gcc@7
brew install dfu-programmer
brew install gcc-arm-none-eabi
brew install avrdude
```

### Windows

[msys2](http://www.msys2.org/) will be used.

1. Visit the [msys2](http://www.msys2.org/) website, and download the installer suited for your PC:
  - 32bit: msys2-i686-xxxxxxx.exe
  - 64bit: msys2-x86_64-xxxxxxxx.exe
1. Launch msys2.
1. Move the QMK firmware folder to the folder (This guide assumes msys2 installed to the C drive): `cd /c/qmk_firmware/`
1. Run `util/msys2_install.sh` 
1. The installer will ask you which packages to install (When in doubt, respond `Y` to install)
1. When complete, restart msys2.

## Build and flash

Run the following at the root directory of the QMK folder:

    make helix:default

To flash at the same time, attach `:avrdude` to the command:

    make helix:default:avrdude

For flashing via GUI, use [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases) as described earlier.

Both halves must be flashed.

## カスタマイズ

/keyboards/helix/rev2/keymaps/ にある default フォルダを複製して好きな名前にします。
以後、それを修正します。

その時のビルドコマンドは以下のようになります。

    make helix:<あなたのkeymap名>

## キーマップを変更する

デフォルトのキーマップは下記のようになっています。これは
keymap.c
を修正することで自由に変更することが出来ます。

キーコードは[リファレンス](https://docs.qmk.fm/keycodes.html)などを参照してください。

![Imgur](https://i.imgur.com/YxZT1TL.png)

## 4行版に対応する

キーマップ内の rules.mk にある HELIX_ROWS を 5 から 4 に変更します。

    HELIX_ROWS = 4

## RGBバックライトを有効にする

キーマップ内の rules.mk にある LED_BACK_ENABLE を no から yes に変更します。

    LED_BACK_ENABLE = yes

##  Underglow を有効にする

キーマップ内の rules.mk にある LED_UNDERGLOW_ENABLE を no から yes に変更します。

    LED_UNDERGLOW_ENABLE = yes

## OLEDを有効にする

キーマップ内の rules.mk にある OLED_ENABLE を no から yes に変更します。

    OLED_ENABLE = yes


### フォントデータのカスタマイズ
フォントデータは helix/common/glcdfont.c です。
こちらを下記のいずれかの方法で編集することでOLED表示のカスタマイズが出来ます。

#### Web Toolで編集

[@teri_yakichan](https://twitter.com/teri_yakichan) さんが作成した、ブラウザでglcdfont.cを編集するツールが便利です。

[Helix Font Editor](http://teripom.x0.com/)

#### 画像エディタで編集

画像エディタを使いたいときは、下記の手順で一旦画像化してから編集し再度テキスト化します。

1. glcdfont.c からデータ部分のみを抜き出してテキストファイルを作る  
0x00, 0x00 ... 0x00
2. スクリプトで画像に変換する
3. 画像を修正する
4. スクリプトでテキストに戻す
5. glcdfont.c に反映させる

編集画像のイメージ

![Font](https://i.imgur.com/adJX6CX.png)

スクリプトはこちらを使用します。
https://github.com/MakotoKurauchi/helix/tree/master/FontConverter

テキストから画像への変換

    $ python3 hex2img.py inHex.txt outImage

画像からテキストへの変換

    $ python3 img2hex.py inImage.bmp > outHex.txt

### キーマップ毎にフォントデータを用意する

helix/common/glcdfont.c を修正してしまうと全てのキーマップに影響が出ます。キーマップ独自のフォントファイルを用意したい時は、まず下記のようにキーマップ内の rules.mk にある LOCAL_GLCDFONT を no から yes に変更します。

    LOCAL_GLCDFONT = yes

次に glcdfont.c を helixfont.h とリネームして keymap.c と同じ階層に複製します。




## それ以外のカスタマイズ

QMKは沢山の機能があります。[リファレンス](https://docs.qmk.fm)や他の人のカスタマイズを参考にして自分だけの最高のHelixを作って下さいね！
