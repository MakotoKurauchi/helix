# ファームウェア

下記よりダウンロードしてください。

https://github.com/qmk/qmk_firmware/

ビルドコマンドは以下のようになります。

    make helix:default

## カスタマイズ

/keyboards/helix/rev2/keymaps/ にある default フォルダを複製して好きな名前にします。
以後、それを修正します。

ビルドコマンドは以下のようになります。

    make helix:<あなたのkeymap名>

## キーマップを変更する

デフォルトのキーマップは下記のようになっています。これは
keymap.c
を修正することで自由に変更することが出来ます。

キーコードは[リファレンス](https://docs.qmk.fm/keycodes.html)などを参照してください。

![Imgur](https://i.imgur.com/YxZT1TL.png)



## RGBバックライト/ Underglow を有効にする

RGBバックライトとUnderglowは、共にQMKの[RGB Lighting](https://docs.qmk.fm/feature_rgblight.html)機能を使っているので設定は共通しています。似た名前で[Backlighting](https://docs.qmk.fm/feature_backlight.html)機能がありますがこちらは使いません。

先ず、rules.mk を修正して機能を有効にします。

    RGBLIGHT_ENABLE = yes

次に config.h で使用するLEDの数と最大の明るさを設定します。
最大の明るさを下記の推奨値以下にしないと消費電流が大きくなり過ぎますのでご注意ください。

バックライトの時

    #define RGBLED_NUM 6
    #define RGBLIGHT_LIMIT_VAL 255

Underglow（5行）の時

    #define RGBLED_NUM 32
    #define RGBLIGHT_LIMIT_VAL 120


Underglow（4行）の時

    #define RGBLED_NUM 25
    #define RGBLIGHT_LIMIT_VAL 130


## OLEDを有効にする

config.h の下記の定義を有効にします。（行頭の「//」を取ります）

    #define SSD1306OLED


### フォントデータのカスタマイズ
フォントデータは helix/common/glcdfont.c です。


カスタマイズ方法
1. glcdfont.c からデータ部分のみを抜き出してテキストファイルを作る  
(0x00, 0x00 ... 0x00)
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
