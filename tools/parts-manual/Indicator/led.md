# マニュアル: LED赤、青

<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="50">

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g112519/)

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" alt="Image from Gyazo" width="500"/>

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| LEDの長い脚（アノード +）  | obnizの0番    |
| LEDの短い脚（カソード -）  | obnizの1番    |

2. 使うノードとつなぎ方
- inject 
- change
- switch
- obniz function 

<a href="https://gyazo.com/58990f620b24d4b55dd3043c05e96cc8"><img src="https://i.gyazo.com/58990f620b24d4b55dd3043c05e96cc8.png" alt="Image from Gyazo" width="600"/></a>

<a href="https://gyazo.com/58990f620b24d4b55dd3043c05e96cc8"><img src="https://i.gyazo.com/58990f620b24d4b55dd3043c05e96cc8.png" alt="Image from Gyazo" width="600"/></a>


3. 各ノードの設定方法
- change
payloadの代入する値を、文字列の `on` とします。

<a href="https://gyazo.com/dc4c766c8fdd4222bacd8355dd282abb"><img src="https://i.gyazo.com/dc4c766c8fdd4222bacd8355dd282abb.gif" alt="Image from Gyazo" width="600"/></a>

- switch

onとoffの分岐を追加します。

<a href="https://gyazo.com/e3891c25bca6fec661a1ec1ee8ee4537"><img src="https://i.gyazo.com/e3891c25bca6fec661a1ec1ee8ee4537.gif" alt="Image from Gyazo" width="600"/></a>


- obniz functionのコード①


```javascript

obnizParts.led.on(); //ledをONにする

```

4. offの分岐を追加する

下記ノードを追加し図のようにつないでください

- inject
- change
- obniz function

<a href="https://gyazo.com/2895856ce7e7039dfb66fe98848aebf6"><img src="https://i.gyazo.com/2895856ce7e7039dfb66fe98848aebf6.gif" alt="Image from Gyazo" width="600"/></a>


- change

代入する値に`off` といれる

- obniz functionのコード②


```javascript

obnizParts.led.off();//ledをOFFにする

```

わかりやすく、ノードに名前をつけておきましょう！

<a href="https://gyazo.com/0b7a879974168b7a4e6365ce3483aab5"><img src="https://i.gyazo.com/0b7a879974168b7a4e6365ce3483aab5.gif" alt="Image from Gyazo" width="600"/></a>


5. 初期化処理コードの編集

```javascript

obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる

```

5. 結果

injectのボタンをクリックしてLEDのON/OFFができればOKです。






■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

</details>