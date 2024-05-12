# マニュアル: 超音波距離センサー

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
