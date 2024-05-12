# マニュアル: サーボモーター

サーボモーターは角度を指定して回転させるモーターです。

**★ 極性(+ -)があるため、ピンの接続に間違えがないか注意**してください。

<img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="50">

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g108761/)



## 1. obnizでの配線



| サーボモーター         | ジャンパワイヤー         | obnizピン|
|--------------|---------------|-------|
| 茶  |   白   |  マイナス-    |
| 橙   |  赤    |  プラス+     |
| 黄   |  青    |  obniz2番     |

サーボモーター茶 - ジャンパワイヤ白
サーボモーター橙 - ジャンパワイヤ赤
サーボモーター黄 - ジャンパワイヤ青

<img src="https://i.gyazo.com/7569445e6968343962bec179da49a56c.jpg" width="500"/>

<img src="https://i.gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461.png" width="500"/>

<img src="https://i.gyazo.com/78e42de894f9c2714afc006e27a0f521.png" width="500"/>


2. 使うノードとつなぎ方
- inject 2つ
- obniz function
- debug

<a href="https://gyazo.com/07730ffe37a53eb5df08aeb35f617eec"><img src="https://i.gyazo.com/07730ffe37a53eb5df08aeb35f617eec.png" alt="Image from Gyazo" width="500"/></a>

3. 各ノードの設定方法

- - inject 2つ

msg.payloadの値を、「数値」「任意の角度」にそれぞれ設定。

例は、30度と90度にサーボモーターを動かす場合

<a href="https://gyazo.com/386a1d891e3183372b7ee03d7ad49881"><img src="https://i.gyazo.com/386a1d891e3183372b7ee03d7ad49881.gif" alt="Image from Gyazo" width="500"/></a>

- obniz function

```javascript

obnizParts.servo.angle(msg.payload); //msg.payloadの角度にサーボモーターを動かす

return msg //msgを出力


```


4. 初期化処理コードの編集

```javascript

obnizParts.servo = obniz.wired("ServoMotor",{ signal:2 }); //サーボモーターをどのくらい回すかの信号を2番に設定


```


5. 結果

■ 参考資料
[obnizの公式ドキュメント: ](https://docs.obniz.com/ja/sdk/parts/ServoMotor/README.md)

</details>

