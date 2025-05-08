# 複数のパーツを同時に使うときのTips

例: Cds(照度センサー)とスピーカーを組み合わせる時  
  
<a href="https://gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef"><img src="https://i.gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef.jpg" alt="Image from Gyazo" width="300"/></a>
  
- obniz 0 - 電圧出力（5V）
- obniz 1 - 電圧入力（CdSと抵抗の**分圧**）
- obniz 2 - 電圧出力（0V）
- obniz 9 - スピーカー
- obniz 11 - スピーカー



初期化処理コードの書き方

```javascript
obniz.io0.output(true); //io0を5vに
obniz.io2.output(false); //io2をGNDに
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 });//9、11番をスピーカーに

```

obnizでは、何番のピンに何を割り当てるかを初期化処理にかいて設定します。


## obniz repeatは複数NG！ひとつにまとめよう。

`obniz repeatノード`を2つ使う場合は注意が必要です。

こんなとき
<a href="https://gyazo.com/83e89db67b9f050293ddf5e835d2962a"><img src="https://i.gyazo.com/83e89db67b9f050293ddf5e835d2962a.png" alt="Image from Gyazo" width="300"/></a>

1つめの`obniz repeatノード`

```javascript
msg.payload = await obnizParts.dht20.getAllDataWait();
return msg;

```

2つめの`obniz repeatノード`
```javascript
const voltage = await obniz.ad1.getWait();

obniz.display.print(voltage)
msg.payload = `changed to ${voltage} v`;
return msg;
```

これだと2個目に入れたCdSしか機能しません。


### 解決策: `obniz repeatノード`は1つにまとめる

#### ダメな例

msg.payloadに2つ値をいれると上書きされてしまいます。

```javascript

msg.payload = await obnizParts.dht20.getAllDataWait();

const voltage = await obniz.ad1.getWait();

obniz.display.print(voltage)
msg.payload = `changed to ${voltage} v`; //上書きされちゃう

return msg;

```

#### OKな例

msg.payloadをまるごと書き換えるのではなく、

`msg.payload.cds` に値を入れてあげるとうまくいきます。


データの構造：

<a href="https://gyazo.com/d00039679887c32f5aed47ce805fe9f3"><img src="https://i.gyazo.com/d00039679887c32f5aed47ce805fe9f3.png" alt="Image from Gyazo" width="228"/></a>

```javascript
msg.payload = await obnizParts.dht20.getAllDataWait();

const voltage = await obniz.ad1.getWait();

obniz.display.print(voltage)
msg.payload.cds = `changed to ${voltage} v`;

return msg;

```

JSONデータの取扱については [ノードが渡すメッセージmsgって何](./lesson03-obniz-advanced/03_obniz-temp.md#ノードが渡すメッセージmsgって何)を参考にしてください。

---

**[◀ 目次ページに戻る](./readme.md)**
