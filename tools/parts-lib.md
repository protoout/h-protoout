# 電子パーツの基本的な使い方一覧

今まで授業内で使った電子パーツや運営側が制作用に準備したパーツの使い方まとめ資料です。

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。


### LED赤、青: 

<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)

<details><summary>使い方をクリックで開く</summary>

1. obnizでの配線

<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" alt="Image from Gyazo" width="500"/>

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| LEDの長い脚  | obnizの0番    |
| LEDの短い脚  | obnizの1番    |

2. 使うノードとつなぎ方
- inject 2つ
- obniz function
- debug

<a href="https://gyazo.com/b685c59d9faa57a0a551037d0caa39e1"><img src="https://i.gyazo.com/b685c59d9faa57a0a551037d0caa39e1.png" alt="Image from Gyazo" width="500"/></a>


3. 各ノードの設定方法
- inject
1つ目: payloadの設定を「真偽」、trueにする
2つ目: payloadの設定を「真偽」、falseにする

<a href="https://gyazo.com/aed583d3a1b5403d933445538a73f7f8"><img src="https://i.gyazo.com/aed583d3a1b5403d933445538a73f7f8.gif" alt="Image from Gyazo" width="500"/></a>

- obniz functionのコード

```javascript
obniz.display.clear(); // 画面を消去

if (msg.payload === true) {
 // スイッチが押されている状態
 obniz.display.print('LED ON');
 obnizParts.led.on();
} else {
 // スイッチが押されていない状態
 obniz.display.print('LED OFF');
 obnizParts.led.off();
}


```


4. 初期化処理コードの編集

```javascript
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 });

```

5. 結果

injectのボタンtrueを押すと光り、falseを押すと消える。


■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

</details>

---

### パトランプ: 

<img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="50">, 出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino)

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

<img src="https://i.gyazo.com/a761dd9b2e6b058523ca062e14adb16d.jpg" alt="img" width= "500">


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  |  obnizの0番    |
|  G  |   obnizの1番   |
|  Y  |   obnizの2番   |
|  R  |   obnizの3番   |



2. 使うノードとつなぎ方
- injection
- obniz function
- debug

<a href="https://gyazo.com/4f52c51092088a407d00b64e5c347a12"><img src="https://i.gyazo.com/4f52c51092088a407d00b64e5c347a12.png" alt="Image from Gyazo" width="500"/></a>

3. 各ノードの設定方法

- injection

<a href="https://gyazo.com/ed7b5fc7363878099a5f6cf42314aae5"><img src="https://i.gyazo.com/ed7b5fc7363878099a5f6cf42314aae5.gif" alt="Image from Gyazo" width="500"/></a>


- obniz function

```javascript

obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる

return msg;


```


4. 初期化処理コードの編集

```javascript

obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:0, green:1, yellow:2, red:3});


```


5. 結果

injectionノードのボタンをクリックすると、赤いLEDが光ります。

injectionノードでpayloadの設定を「green」「yellow」に変更すると、違う色のLEDが光ります。


■ 参考資料
[obnizの公式ドキュメント: Keyestudio TrafficLight](https://docs.obniz.com/ja/sdk/parts/Keyestudio_TrafficLight/README.md)

</details>

---

### 温湿度センサ: 

<img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

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

msg.payload = await obnizParts.dht20.getAllDataWait();

return msg;

```


4. 初期化処理コードの編集

```javascript

obnizParts.dht20 = obniz.wired("DHT20",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: "5v"});


```


5. 結果

湿度と温度が表示されればOK。


<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>


■ 参考資料
[データの中から特定の数値のみ取り出して使う方法: JSONデータの扱いについて」](./json-data.md)

</details>

---

### 超音波距離センサー: 

<img src="https://akizukidenshi.com/img/goods/L/111009.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)


超音波を発生し、物体に当たってから跳ね返ってくるまでの時間を計測することで、その対象物体との距離を算出できます。
距離を測るだけでなく、単純に目の前に人がいるかいないか、といった用途にも使えます。


<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
|  Gnd |  obnizの0番    |
|  Echo  |   obnizの1番   |
|  Trig  |   obnizの2番   |
|  Vcc  |   obnizの3番   |

2. 使うノードとつなぎ方

- obniz repeat
- dedbug

<a href="https://gyazo.com/f12a5b25d4c360c7e545ededed17019e"><img src="https://i.gyazo.com/f12a5b25d4c360c7e545ededed17019e.png" alt="Image from Gyazo" width="520"/></a>



3. 各ノードの設定方法

- obniz repeat

コードを書き換える

```javascript

msg.payload = await obnizParts.hcsr04.measureWait();

return msg;

```

Intervalを書き換える。

単位はms（1000ms = 1秒）です。

図は1秒に1回取得する場合の設定です。

<a href="https://gyazo.com/8604f33b379baf4a666be0ab85ffdb16"><img src="https://i.gyazo.com/8604f33b379baf4a666be0ab85ffdb16.png" alt="Image from Gyazo" width="648"/></a>


4. 初期化処理コードの編集

```javascript

obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 });


```


5. 結果

コンソールに距離の数値がでてくれば成功です！


■ 参考資料
[obnizの公式ドキュメント: 距離センサー](https://docs.obniz.com/ja/guides/obniz-starter-kit/use-parts/distance)
[取得した数値データを四捨五入したい: 計算処理いろいろ](./math-data.md)
[取得したデータをテンプレートにはめ込んで表示したい](./math-data.md)


</details>


---


### 照度センサー(CdS): 

<img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|   |      |
|    |      |

2. 使うノードとつなぎ方

3. 各ノードの設定方法


```javascript

```


4. 初期化処理コードの編集

```javascript

```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ]()

</details>

---


### サーボモーター: 

<img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|   |      |
|    |      |

2. 使うノードとつなぎ方

3. 各ノードの設定方法


```javascript

```


4. 初期化処理コードの編集

```javascript

```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ]()

</details>



---


### スピーカー（ブザー）: 

<img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|   |      |
|    |      |

2. 使うノードとつなぎ方

3. 各ノードの設定方法


```javascript
obnizParts.Speaker.play(1000); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
speaker.stop(); // 音を止める
```


4. 初期化処理コードの編集

9番と11番に接続する例です。

```javascript
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 });
```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ]()

</details>



---


### obnizのディスプレイ: 

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|   |      |
|    |      |

2. 使うノードとつなぎ方

3. 各ノードの設定方法


```javascript

```


4. 初期化処理コードの編集

```javascript

```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ]()

</details>


---


### obnizのスイッチ: 

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|   |      |
|    |      |

2. 使うノードとつなぎ方

3. 各ノードの設定方法


```javascript

```


4. 初期化処理コードの編集

```javascript

```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ]()

</details>



---
