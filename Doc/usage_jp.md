# 使い方

Helixの使い方をデフォルトキーマップで説明します。

## 左右の接続

左右の接続には3極（TRS）もしくは4極（TRRS）のステレオオーディオミニプラグを使用します。  
（LEDやOLEDを使用する場合でも3極で問題ありません）

※故障する恐れがありますのでUSBケーブルを繋げたままでの挿抜はしないでください。

![Imgur](https://i.imgur.com/1alxKG2.jpg)


## レイヤー

Helixは通常のキーボードと比較して明らかにキーの数が足りません。  
キーマップはレイヤーを重ねた多層構造になっており、収まらないキーやHelixの設定を変える機能キーは別のレイヤーに入っています。

|優先順位|レイヤー番号|レイヤー名|内容|
| ---- | ---- | --- | --- |
|高い|5|Adjust|機能キー|
||4|Raise|記号類（ピンク）|
||3|Lower|記号類（ブルー）|
||2|Dvorak|Dvorak配列|
||1|Colemak|Colemak配列|
|低い|0|Qwerty|QWERTY配列（ベース）|


ベースレイヤー以外は普段は隠れていますが、対応するレイヤーキーを押すことで現在の配列の上にそのレイヤーが現れます。重なったところは、レイヤー番号が大きいほうが優先順位が高くなりますので、キーコードが変わることになります。

具体例をあげると、RaiseとLowerをQwertyに重ねたのが下の画像です。  
例えばピンクのRaiserキーを押しながらaを押すと、F1キーなります。

![Imgur](https://i.imgur.com/10R4O2P.jpg)

次にAdjustとQwertyを重ねたのが下の画像です。  
例えばAdjustを押しながらqを押すとキーボードがリセットされ、書き込みモードになります。（リセットスイッチを押したときと同じ状態）

![Imgur](https://i.imgur.com/jaYTsNM.png)

また、デフォルトキーマップでは、Lower + Raiseの同時押しはAdjustとなるようにしています。


## LEDコントロール

バックライトやUnderglowをコントロールするにはAdjustレイヤーにある機能キーを使います。

|コマンド|デフォルトレイアウト|コード|
| ---- | ---- | --- |
|オン／オフ|Adjust + ,|RGB_TOG|
|モード|Adjust + Left|RGB_SMOD|
|リセット|Adjust + w|RGBRST|
|色相 +|Adjust + .|RGB_HUI|
|色相 -|Adjust + Down|RGB_HUD|
|彩度 +|Adjust + /|RGB_SAI|
|彩度 -|Adjust + Up|RGB_SAD|
|明度 +|Adjust + Enter|RGB_VAI|
|明度 -|Adjust + Right|RGB_VAD|

## MacモードとWinモードの切り替え

MacモードはEISUキーとKANAキーがそれぞれ英数キーとかなキーとして入力されます。

WinモードはEISUキーとKANAキーが共に Alt + `（日本語IMEの切り替え）として入力されます。  
また、<font color="Red">AltキーとGUIキーが入れ替わります</font>。

現在のモードはOLEDにアイコンとして表示されます。

|コマンド|デフォルトレイアウト|コード|
| ---- | ---- | --- |
|Macモード|Adjust + g|AG_NORM|
|Winモード|Adjust + h|AG_SWAP|
