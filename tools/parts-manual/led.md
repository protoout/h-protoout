# マニュアル: LED赤、青

<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g112519/)

<details><summary>使い方をクリックで開く</summary>


1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" alt="Image from Gyazo" width="500"/>

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| LEDの長い脚（アノード +）  | obnizの0番    |
| LEDの短い脚（カソード -）  | obnizの1番    |

2. 使うノードとつなぎ方
- inject 2つ
- switch ※switchノードは設定後にノードをつなぐ
- obniz function 2つ
- debug

<a href="https://gyazo.com/a4746c59ffd824626fe0f679c1c8e8d9"><img src="https://i.gyazo.com/a4746c59ffd824626fe0f679c1c8e8d9.png" alt="Image from Gyazo" width="774"/></a>


3. 各ノードの設定方法
- inject
1つ目: payloadの設定を「真偽」、trueにする
2つ目: payloadの設定を「真偽」、falseにする

<a href="https://gyazo.com/4014ae3108033b8aab83e8f437aebb42"><img src="https://i.gyazo.com/4014ae3108033b8aab83e8f437aebb42.gif" alt="Image from Gyazo" width="500"/></a>


- switch

分岐を追加する。

<a href="https://gyazo.com/aa07ff50cc9cae349e1bbced481dfb8a"><img src="https://i.gyazo.com/aa07ff50cc9cae349e1bbced481dfb8a.gif" alt="Image from Gyazo" width="500"/></a>

その後、obniz functionノードにつないでください。

<a href="https://gyazo.com/d9ac82738971e5aa0c4af8ef34571749"><img src="https://i.gyazo.com/d9ac82738971e5aa0c4af8ef34571749.gif" alt="Image from Gyazo" width="500"/></a>


- obniz functionのコード①


```javascript

obnizParts.led.on(); //ledをONにする

```

- obniz functionのコード②


```javascript

obnizParts.led.off();//ledをOFFにする

```


4. 初期化処理コードの編集

```javascript

obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる

```

5. 結果

injectのボタンtrueを押すと光り、falseを押すと消える。


■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

</details>