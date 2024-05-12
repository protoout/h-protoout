# obnizで複数のパーツを同時に使いたい

ここではobnizで複数のパーツを同時に使うときの手順を説明します。

1. 配線します


<a href="https://gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef"><img src="https://i.gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef.jpg" alt="Image from Gyazo" width="300"/></a>

- obniz 0 - 電圧出力（5V）（写真 ジャンパワイヤ赤）
- obniz 1 - 電圧入力 （写真 ジャンパワイヤ白）
- obniz 2 - 電圧出力（0V）（写真 ジャンパワイヤ黒）
- obniz 9 - スピーカー
- obniz 11 - スピーカー


2. 初期化処理コードでピンアサインする

obnizでは、何番のピンに何を割り当てるかを初期化処理にかいて設定します。

このとき、必ずピンが被らないようにしてください。


```javascript
obniz.io0.output(true); //io0を5vに
obniz.io2.output(false); //io2をGNDに
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 });//9、11番をスピーカーに

```

