# L01-生成AI: 生成AIと一緒にNode-REDでIoT開発 3/3

引き続きやっていきます。ここではいよいよセンサーに接続してみます。

## 3. 距離センサーが反応したら音を出す

### 3-1. 距離センサーとスピーカーの配線

**ここからはセンサーは貸し合って試してみてください。**

写真のように配線してみましょう。

<img src="https://i.gyazo.com/53bb7be7ba1d99ed2934715654e4b1f3.png" width="400px" />

- 0,1,2,3ピンに超音波距離センサー
- 9,11ピンにスピーカー

を繋げてみます。

### 3-1. 距離センサーに差し替え

エミュレートで使っていた`injectノード`,`changeノード`を`obniz repeatノード`に入れ替えましょう。

<img src="https://i.gyazo.com/d4fb9397dff4fbfcf93c7f26d5da1117.png" width="400px" />

[超音波距離センサーのマニュアルページ](../../../tools/parts-manual/sensor/distance.md)を参考に`設定ノード`と`obniz repeatノード`に中身をコピペします。

- `設定ノード`の初期化処理

```js
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //0,1,2,3番にピンを割り当てる
```

- `obniz repeatノード`

```js
msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力
```

### 3-2

及び[スピーカーのマニュアルページ](../../../tools/parts-manual/actuator/speaker.md)

### 3-
こんな感じでステップを踏んでフローを変えてきたイメージがなんとなく掴めていると嬉しいです。

> <img src="https://i.gyazo.com/fbdcafe1eacd1e10bb644d620ab35a4a.png" width="400px" />


**[◀ 目次ページに戻る](../readme.md)**