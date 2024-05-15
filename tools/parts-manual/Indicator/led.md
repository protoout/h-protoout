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
- switch ※switchノードは設定後にノードをつなぐ
- obniz function 2つ

<a href="https://gyazo.com/80cebbe41de81925a0908545f8f8058f"><img src="https://i.gyazo.com/80cebbe41de81925a0908545f8f8058f.gif" alt="Image from Gyazo" width="600"/></a>

3. 各ノードの設定方法

- switch

<a href="https://gyazo.com/db8c1564785fa06baa4ea2738b9b8d97"><img src="https://i.gyazo.com/db8c1564785fa06baa4ea2738b9b8d97.gif" alt="Image from Gyazo" width="600"/></a>


- change

<a href="https://gyazo.com/76c8b7748d4544d6fa50fb7d9767468a"><img src="https://i.gyazo.com/76c8b7748d4544d6fa50fb7d9767468a.gif" alt="Image from Gyazo" width="1000"/></a>



- obniz functionのコード①


```javascript

obnizParts.led.on(); //ledをONにする

```
- obniz functionのコード②


```javascript

obnizParts.led.off();//ledをOFFにする

```

- inject

名前を変更しておきましょう

<a href="https://gyazo.com/2a5337ef111f1a28b91a44768f44f676"><img src="https://i.gyazo.com/2a5337ef111f1a28b91a44768f44f676.gif" alt="Image from Gyazo" width="600"/></a>


4. 初期化処理コードの編集

```javascript

obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる

```

5. 結果

ONを押すと光り、OFFを押すと消える。

■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

</details>