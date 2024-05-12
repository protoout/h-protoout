# 電子パーツの基本的な使い方一覧

今まで授業内で使った電子パーツや運営側が制作用に準備したパーツの使い方まとめ資料です。

## LED赤、青: 

使い方は[こちら](./led.md)です。

> <img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="50">

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g112519/)

## サーボモーター: 

使い方は[こちら](./servo.md)です。

> <img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="50">
> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g108761/)

## パトランプ: 

使い方は[こちら](./ledlights.md)です。

> <img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="50">

> 出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino)

---

### 温湿度センサー: 

<img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g116732/)

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違えがないか注意**


温湿度センサーの穴が空いている面からみて、左からobnizの0,1,2,3の順で繋いでください。


<a href="https://gyazo.com/66d9746a30db63c1e7f5aa03c6fbf614"><img src="https://i.gyazo.com/66d9746a30db63c1e7f5aa03c6fbf614.png" alt="Image from Gyazo" width="145"/></a>


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
|  1 |  obnizの0番    |
|  2  |   obnizの1番   |
|  3  |   obnizの2番   |
|  4  |   obnizの3番   |


<a href="https://gyazo.com/e97a9e811cfe8957128826720f509d20"><img src="https://i.gyazo.com/e97a9e811cfe8957128826720f509d20.jpg" alt="Image from Gyazo" width="500"/></a>
<a href="https://gyazo.com/634598ac1868f02bbd4100bd06af5a89"><img src="https://i.gyazo.com/634598ac1868f02bbd4100bd06af5a89.png" alt="Image from Gyazo" width="500"/></a>


※直接obnizにさしても動きますが、少しゆるいためブレッドボードを使います。

2. 使うノードとつなぎ方

- obniz repeat
- debug


<a href="https://gyazo.com/fde72c61d77a840518cbcf1f1122efdf"><img src="https://i.gyazo.com/fde72c61d77a840518cbcf1f1122efdf.png" alt="Image from Gyazo" width="500"/></a>


3. 各ノードの設定方法

- obniz repeat

```javascript

msg.payload = await obnizParts.dht20.getAllDataWait(); //温湿度センサーの値を、msg.payloadに格納する

return msg; //msg.payloadを出力する

```


4. 初期化処理コードの編集

0番、1番、2番、3番に接続した場合の例

```javascript

obnizParts.dht20 = obniz.wired("DHT20",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: "5v"}); //0,1,2,3番にピンをアサインし、電圧を5Vに設定


```


5. 結果

湿度と温度が表示されればOK。


<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>


■ 参考資料
[データの中から特定の数値のみ取り出して使う方法: JSONデータの扱いについて」](./json-data.md)

</details>

---

### 超音波距離センサー: 

<img src="https://akizukidenshi.com/img/goods/L/111009.jpg" width="50">, 出典：[秋月電子通商](http://akizukidenshi.com/catalog/g/gM-11009/)


<details><summary>使い方をクリックで開く</summary>

超音波を発生し、物体に当たってから跳ね返ってくるまでの時間を計測することで、その対象物体との距離を算出できます。
距離を測るだけでなく、単純に目の前に人がいるかいないか、といった用途にも使えます。


1. obnizでの配線

<a href="https://gyazo.com/333e9751bf9f478ed388bc6bda7fa691"><img src="https://i.gyazo.com/333e9751bf9f478ed388bc6bda7fa691.jpg" alt="Image from Gyazo" width="500"/></a>

**★ 極性(+ -)があるため、接続に間違えがないか注意**


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
|  Gnd |  obnizの8番    |
|  Echo  |   obnizの9番   |
|  Trig  |   obnizの10番   |
|  Vcc  |   obnizの11番   |



2. 使うノードとつなぎ方

- obniz repeat
- dedbug

<a href="https://gyazo.com/f12a5b25d4c360c7e545ededed17019e"><img src="https://i.gyazo.com/f12a5b25d4c360c7e545ededed17019e.png" alt="Image from Gyazo" width="520"/></a>



3. 各ノードの設定方法

- obniz repeat

コードを書き換える

```javascript

msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力

```

Intervalを書き換える。

単位はms（1000ms = 1秒）です。

図は1秒に1回取得する場合の設定です。

<a href="https://gyazo.com/8604f33b379baf4a666be0ab85ffdb16"><img src="https://i.gyazo.com/8604f33b379baf4a666be0ab85ffdb16.png" alt="Image from Gyazo" width="648"/></a>


4. 初期化処理コードの編集

8番,9番,10番,11番に接続する例です。

```javascript

obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:8, echo:9, trigger:10, vcc:11 }); //8,9,10,11番にピンを割り当てる


```


5. 結果

コンソールに距離の数値がでてくれば成功です！


■ 参考資料
[obnizの公式ドキュメント: 距離センサー](https://docs.obniz.com/ja/guides/obniz-starter-kit/use-parts/distance)
[取得した数値データを四捨五入したい: 計算処理いろいろ](./math-data.md)

</details>


---


### 照度センサー(CdS): 

<img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g100110/)
<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

★極性なし



| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|  ジャンパワイヤ赤 |   obnizの0番   |
|   ジャンパワイヤ白 |  obnizの1番    |
|   ジャンパワイヤ黒 |  obnizの2番    |

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg" width="500">


<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg" width="500">



2. 使うノードとつなぎ方

- obniz repeat
- debug

<a href="https://gyazo.com/d324617577c3c0af6a86362a49f3509b"><img src="https://i.gyazo.com/d324617577c3c0af6a86362a49f3509b.png" alt="Image from Gyazo" width="500"/></a>

3. 各ノードの設定方法


- obniz repeat

```javascript

var voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

obniz.display.print(voltage)
msg.payload = voltage;

return msg;

```

ad1: Analogデータ（光の強さ）をDigital信号に変換して取得する1番、の意味

6番から分圧の値を取得する場合は、ad6とします。

```javascript
var voltage = await obniz.ad6.getWait(); //ピン6からアナログ（光の強さ）をデジタル信号に変換した値を取得

```



4. 初期化処理コードの編集

```javascript

obniz.io0.output(true); //io0番を5vに
obniz.io2.output(false); //io2番をGNDに


```

赤い線を5番に、白い線を7番につなぐ場合は下記のように変更してください。

```javascript

obniz.io5.output(true); //io5番を5vに
obniz.io7.output(false); //io7番をGNDに


```



5. 結果

明るさに応じてコンソールに表示されている数値が変動すれば成功です。

■ 参考資料
[obnizの公式ドキュメント: obniz AD](https://docs.obniz.com/ja/reference/common/ad)

</details>

---




---


### スピーカー（ブザー）: 

<img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="50">, 出典：[秋月電子通商](http://akizukidenshi.com/catalog/g/gP-04118/)
<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

<a href="https://gyazo.com/081b807593f7bf2ab4725e5d44952a99"><img src="https://i.gyazo.com/081b807593f7bf2ab4725e5d44952a99.jpg" alt="Image from Gyazo" width="500"/></a>

★ 極性(+ -)なし


| 電子パーツの脚         | 接続先         |
|--------------|---------------|
| スピーカーの脚 |   5   |
| スピーカーの脚  |   6   |


2. 使うノードとつなぎ方

- inject
- obniz function

<a href="https://gyazo.com/73e158660e203bf7934600714130de7d"><img src="https://i.gyazo.com/73e158660e203bf7934600714130de7d.png" alt="Image from Gyazo" width="400"/></a>

3. 各ノードの設定方法

- inject

msg.payloadを「数値」「1000」（数字は任意で変更してください。単位はヘルツ。）

<a href="https://gyazo.com/7cbace6d7c01f7290f91907f14c2bd87"><img src="https://i.gyazo.com/7cbace6d7c01f7290f91907f14c2bd87.gif" alt="Image from Gyazo" width="500"/></a>


- obniz function

```javascript
obnizParts.Speaker.play(msg.payload); // msg.payloadで受け取った値（ヘルツ）の音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.stop(); //止める
```


4. 初期化処理コードの編集

5番と6番に接続する例です。

```javascript
obnizParts.Speaker = obniz.wired("Speaker",{ signal:5, gnd:6 }); 
```


5. 結果

1000Hzの音が鳴り、1秒すると止まる。


■ 参考資料
[obnizの公式ドキュメント: ](https://docs.obniz.com/ja/sdk/parts/Speaker/README.md)

- 音階の表


| 音階 | 周波数[Hz] |
| ---- | ---------- |
| ド   | 523        |
| レ   | 587        |
| ミ   | 659        |
| ファ | 698        |
| ソ   | 784        |
| ラ   | 880        |
| シ   | 988        |
| ド   | 1046       |


ドレミを1秒ずつ鳴らすサンプル

```javascript

obnizParts.Speaker.play(523); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.play(587); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.play(659); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.Speaker.stop(); 

```


</details>
