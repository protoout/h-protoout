# ガスセンサー MQ135

> 高い感度で様々なガスに反応するセンサーで、特に大気汚染物質であるNH3, NOx, 煙, Co2などに反応します。
> このセンサーは加熱を必要とします。十分に加熱されないと値は安定しません（少なくとも2分程度）
> このライブラリでは、出力値の電圧のみ取得できますので、ガスの濃度が上がるほど電圧が上がっていきます。また、実際のガスの濃度(ppm)に変換したい場合はキャリブレーションを行い、計算式で変換する必要があります。


<img src="https://docs.obniz.com/ja/sdk/parts/MQ135/image.jpg" width="100">, 出典：[obniz Parts Library](https://docs.obniz.com/ja/sdk/parts/MQ135/README.md)



## 1. obnizでの配線

<details><summary>配線の仕方をクリックで開く</summary>

<a href="https://gyazo.com/1bb0746a755d99f23d844733a95ef9ed"><img src="https://i.gyazo.com/1bb0746a755d99f23d844733a95ef9ed.jpg" alt="Image from Gyazo" width="708"/></a>

**★ 極性(+ -)があるため、接続に間違えがないか注意**


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
|  vcc |  obnizの3番    |
|  gnd  |   obnizの2番   |
|  do  |   obnizの1番   |
|  ao  |   obnizの0番   |

</details>

## 2. 使うノードとつなぎ方

<details><summary>ノードの繋ぎ方をクリックで開く</summary>
- obniz repeat
- dedbug

<a href="https://gyazo.com/f12a5b25d4c360c7e545ededed17019e"><img src="https://i.gyazo.com/f12a5b25d4c360c7e545ededed17019e.png" alt="Image from Gyazo" width="520"/></a>

</details>

## 3. 各ノードの設定方法

- obniz repeat

コードを書き換える

```javascript

obnizParts.mq135.onchangeanalog = function(voltage) {
  msg.payload =voltage; //取得した値をmsg.payloadに格納
};

return msg;



```

Intervalを書き換える。

単位はms（1000ms = 1秒）です。

図は1秒に1回取得する場合の設定です。

<a href="https://gyazo.com/8604f33b379baf4a666be0ab85ffdb16"><img src="https://i.gyazo.com/8604f33b379baf4a666be0ab85ffdb16.png" alt="Image from Gyazo" width="648"/></a>


## 4. 初期化処理コードの編集

3番,2番,1番,0番に接続する例です。

```javascript

obnizParts.mq135 = obniz.wired("MQ135", {vcc:3, gnd:2, do:1, ao:0});
await obnizParts.mq135.heatWait(); //加熱開始。十分に加熱されると計測ができます。

```


## 5. 結果

開始してから2分ほど、加熱を行い、十分に加熱されてから計測されます。

**※ 火傷に注意してください！**



コンソールに距離の数値がでてくれば成功です！


■ 参考資料
[obnizの公式ドキュメント: 距離センサー](https://docs.obniz.com/ja/guides/obniz-starter-kit/use-parts/distance)
[取得した数値データを四捨五入したい: 計算処理いろいろ](./math-data.md)



---
