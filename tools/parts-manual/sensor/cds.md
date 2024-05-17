# マニュアル: 照度センサー(CdS): 

<img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g100110/)
## 1. obnizでの配線

★極性なし
<details><summary>配線の仕方をクリックで開く</summary>

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
|  ジャンパワイヤ赤 |   obnizの0番   |
|   ジャンパワイヤ白 |  obnizの1番    |
|   ジャンパワイヤ黒 |  obnizの2番    |

<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg" width="500">


<img src="https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg" width="500">

</details>

## 2. 使うノードとつなぎ方

<details><summary>ノードの繋ぎ方をクリックで開く</summary>
- obniz repeat
- debug

<a href="https://gyazo.com/d324617577c3c0af6a86362a49f3509b"><img src="https://i.gyazo.com/d324617577c3c0af6a86362a49f3509b.png" alt="Image from Gyazo" width="500"/></a>

</details>

## 3. 各ノードの設定方法


- obniz repeat

```javascript

var voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

msg.payload = voltage;

return msg;

```

ad1: Analogデータ（光の強さ）をDigital信号に変換して取得する1番、の意味

6番から分圧の値を取得する場合は、ad6とかきかえます。

```javascript
const voltage = await obniz.ad6.getWait(); //ピン6からアナログ（光の強さ）をデジタル信号に変換した値を取得

```



## 4. 初期化処理コードの編集

```javascript

obniz.io0.output(true); //io0番を5vに
obniz.io2.output(false); //io2番をGNDに


```

※ 赤い線を5番に、白い線を7番につなぐ場合の書き方

```javascript

obniz.io5.output(true); //io5番を5vに
obniz.io7.output(false); //io7番をGNDに


```



## 5. 結果

明るさに応じてコンソールに表示されている数値が変動すれば成功です。



■ 参考資料
[obnizの公式ドキュメント: obniz AD](https://docs.obniz.com/ja/reference/common/ad)


---




