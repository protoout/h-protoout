# マニュアル: 温湿度センサー

<img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g116732/)

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違えがないか注意**

<details><summary>ノードの繋ぎ方をクリックで開く</summary>
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

</details>

## 2. 使うノードとつなぎ方

<details><summary>ノードの繋ぎ方をクリックで開く</summary>

- obniz repeat
- debug


<a href="https://gyazo.com/fde72c61d77a840518cbcf1f1122efdf"><img src="https://i.gyazo.com/fde72c61d77a840518cbcf1f1122efdf.png" alt="Image from Gyazo" width="500"/></a>

</details>

## 3. 各ノードの設定方法

- obniz repeat

interval(ms)は500くらいに設定しておいてください。

```javascript

msg.payload = await obnizParts.dht20.getAllDataWait(); //温湿度センサーの値を、msg.payloadに格納する

return msg; //msg.payloadを出力する

```


## 4. 初期化処理コードの編集

0番、1番、2番、3番に接続した場合の例

```javascript

obnizParts.dht20 = obniz.wired("DHT20",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: "5v"}); //0,1,2,3番にピンをアサインし、電圧を5Vに設定


```


## 5. 結果

湿度と温度が表示されればOK。


<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>


■ 参考資料
[データの中から特定の数値のみ取り出して使う方法: JSONデータの扱いについて」](./json-data.md)


---
