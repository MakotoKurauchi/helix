# ファームウェア

## とりあえず動作を確認したい

[QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)を使えばビルドなどの手順を踏まずにキーボードとしての動作を確認出来ます。

![Imgur](https://i.imgur.com/MiVj7jo.png)

1. atmega32u4 になってるか確認します
2. helix/rev2 にします
3. Loadボタンを押しダウンロードします


![Imgur](https://i.imgur.com/hLygSgB.png)

1. Helixのリセットボタンを押し、Connected とメッセージが出るのを確認します
2. すぐにFlashボタンを押します

![Imgur](https://i.imgur.com/dH2Wser.png)

このようなメッセージが出れば書き込み終了です

Helixで文字が打てるようになったでしょうか？

配列を変えたり、LEDやOLEDを使いたいときは次から説明するファームウェアのビルドに挑戦してみましょう。

## カスタマイズしたい時
下記ページよりQMKファームウェアをダウンロードします。

https://github.com/qmk/qmk_firmware/

（緑色の"Clone or download"ボタンをクリックし、"Download ZIP"をもう一度クリックしてZIPファイルをダウンロードします。）

そしてダウンロードしたZIPファイルを好きな場所へ伸張しておきます。

gitに慣れている方はクローンの方が良いでしょう。

## ビルド環境を作る
### macOS
 [homebrew](https://brew.sh)を使う手順を説明します。
1. ターミナルを起動します
1. [homebrew](https://brew.sh)を使っていなかったらインストールしておきます
1. 次に下記のコマンドをそれぞれ実行します

```brew tap osx-cross/avr
brew tap PX4/homebrew-px4
brew update
brew install avr-gcc
brew install dfu-programmer
brew install gcc-arm-none-eabi
brew install avrdude
```

### Windows

[msys2](https://github.com/qmk/qmk_firmware/blob/master/docs/getting_started_build_tools.md)を使う手順を説明します。

1. [msys2](https://github.com/qmk/qmk_firmware/blob/master/docs/getting_started_build_tools.md)のサイトに行き、OSに合わせたインストーラをダウンロード＆インストールします。
  - 32bit OSの時 : msys2-i686-xxxxxxx.exe
  - 64bit OSの時 : msys2-x86_64-xxxxxxxx.exe
1. msys2を起動します
1. ダウンロードしておいたQMKファームウェアのフォルダに移動します（ここではcドライブ直下にあるものとします）`cd /c/qmk_firmware/`
1. `util/msys2_install.sh` と実行します
1. インストールするパッケージを聞かれますので答えていきます（分からなければ全て`Y`とします）
1. 終わったらmsys2を再起動します

## ビルドと書き込み

QMKファームウェアの第一階層で以下のようにします。

    make helix:default

キーボードへの書き込みまで同時に行うには下記のように`:avrdude`を付けます。

    make helix:default:avrdude

GUIでの書き込みには冒頭で説明した[QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)が使えます。

左右のキーボードとも同様に書き込みが必要です。

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

キーマップ内のconfig.hにあるHELIX_ROWSを5から4に変更します。

    #define HELIX_ROWS 4

## RGBバックライト/ Underglow を有効にする

RGBバックライトとUnderglowは、共にQMKの[RGB Lighting](https://docs.qmk.fm/feature_rgblight.html)機能を使っているので設定は共通しています。似た名前で[Backlighting](https://docs.qmk.fm/feature_backlight.html)機能がありますがこちらは使いません。

先ず、キーマップ内の rules.mk を修正して機能を有効にします。

    RGBLIGHT_ENABLE = yes
 
次に config.h で使用するLEDの数を設定します。

Underglowの時

    #define RGBLED_NUM 6

バックライト（5行）の時

    #define RGBLED_NUM 32

バックライト（4行）の時

    #define RGBLED_NUM 25


## OLEDを有効にする

config.h の下記の定義を有効にします。（行頭の「//」を取ります）

    #define SSD1306OLED


### フォントデータのカスタマイズ
フォントデータは helix/common/glcdfont.c です。


#### カスタマイズ方法
1. glcdfont.c からデータ部分のみを抜き出してテキストファイルを作る  
0x00, 0x00 ... 0x00
2. スクリプトで画像に変換する
3. 画像を修正する
4. スクリプトでテキストに戻す
5. glcdfont.c に反映させる



![Font](https://i.imgur.com/adJX6CX.png)

テキストから画像への変換

    python3 hex2img.py inHex.txt outImage

画像からテキストへの変換

    python3 img2hex.py inImage.bmp > outHex.txt





## それ以外のカスタマイズ

QMKは沢山の機能があります。[リファレンス](https://docs.qmk.fm)や他の人のカスタマイズを参考にして自分だけの最高のHelixを作って下さいね！
