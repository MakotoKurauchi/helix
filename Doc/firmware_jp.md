# ファームウェア

## とりあえず動作を確認したい

[QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)を使えばビルドなどの手順を踏まずにキーボードとしての動作を確認出来ます。

![Imgur](https://i.imgur.com/75BHCKI.png)

1. atmega32u4 になってるか確認します
2. Helixの構成に合わせて下記のいずれかのHexファイルをダウンロードし、Openボタンでそのファイルを選択してください。


- オプション無し: [helix_rev2_default.hex](http://qmk.fm/compiled/helix_rev2_default.hex)
- 5行版 OLED & バックライト: [helix_rev2_default_oled_backlight.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_oled_backlight.hex)
- 5行版 OLED & Underglow: [helix_rev2_default_oled_underglow.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_oled_underglow.hex)
- 4行版 OLED & バックライト: [helix_rev2_default_4rows_oled_backlight.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_4rows_oled_backlight.hex)
- 4行版 OLED & Underglow: [helix_rev2_default_4rows_oled_underglow.hex](https://raw.githubusercontent.com/MakotoKurauchi/helix/master/Hex/helix_rev2_default_4rows_oled_underglow.hex)
-
![Imgur](https://i.imgur.com/hLygSgB.png)

1. Helixのリセットボタンを押し、Connected とメッセージが出るのを確認します
2. すぐにFlashボタンを押します

![Imgur](https://i.imgur.com/dH2Wser.png)

このようなメッセージが出れば書き込み終了です

Helixで文字が打てるようになったでしょうか？

配列を変えたいときは次から説明するファームウェアのビルドに挑戦してみましょう。


## ビルド環境を作る

QMKの公式ガイドに従いビルド環境を作ります。

https://docs.qmk.fm/#/ja/newbs_getting_started

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

キーコードは[リファレンス](https://docs.qmk.fm/#/keycodes)などを参照してください。

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

[Helix Font Editor](https://helixfonteditor.netlify.com/)

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
