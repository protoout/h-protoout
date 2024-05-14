# マニュアル: タクティルスイッチ（タクトスイッチ）

サーボモーターは角度を指定して回転させるモーターです。

極性(+ -)はありませんが、スイッチの向きには注意しましょう。

> <img src="https://akizukidenshi.com/img/goods/L/103647.jpg" width="50">

> 出典：[秋月電子通商](https://akizukidenshi.com/catalog/g/g103647/)

--(以下WIP)

## 1. obnizでの配線

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。
ジャンパワイヤーの色は何色でも大丈夫です。

<details><summary>配線の仕方をクリックで開く</summary>

| サーボモーター         | ジャンパワイヤー         | obnizピン|
|--------------|---------------|-------|
| 茶  |   白   |  マイナス-    |
| 橙   |  赤    |  プラス+     |
| 黄   |  青    |  obniz2番     |

写真上では以下の配線にしてあります。

- サーボモーター茶 - ジャンパワイヤ白
- サーボモーター橙 - ジャンパワイヤ赤
- サーボモーター黄 - ジャンパワイヤ青

真似して配線してみてください。

> <img src="https://i.gyazo.com/7569445e6968343962bec179da49a56c.jpg" width="300px"/>

> <img src="https://i.gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461.png" width="500"/>

> <img src="https://i.gyazo.com/78e42de894f9c2714afc006e27a0f521.png" width="500"/>

</details>

## 2. 使うノードとつなぎ方
[Node-REDのobnizノードでどちらのノードを選ぶか - 使い方概要](https://qiita.com/n0bisuke/items/072a8a1bf77525fef835)を参考に、使うobnizノードを決めます。今回はアクチュエーターになるので`obniz functionノード`が適しています。

<details><summary>ノードの繋ぎ方をクリックで開く</summary>

### 2-1. obniz functionノードの基本

まずは、以下の3つのノードを使います。

- `injectノード`
- `obniz functionノード`
- `debugノード`

以下のように設置して線で繋ぎましょう。

> <img src="https://i.gyazo.com/2eb9c633060a8af0e92642a3e30d0be3.gif" width="400px" />

`obniz functionノード`を追加したら**obniz IDの設定**を忘れずに行って下さい。この設定も[参考記事](https://qiita.com/n0bisuke/items/072a8a1bf77525fef835)を読んでおきましょう。

### 2-2. chageノードを追加

次に`chageノード`を追加して`20`などの数字を代入します。
代入する値の項目を`数値`に変更しましょう。

> <img src="https://i.gyazo.com/27f6c8330de4b466778b7ee5d6b3d800.gif" width="400px" />

</details>

## 3. 設定ノードとobniz functionノードに処理を記述

それぞれ以下のコードを記述して下さい。

- `obniz functionノード`

```javascript

obnizParts.servo.angle(msg.payload); //msg.payloadの角度にサーボモーターを動かす

return msg //msgを出力
```

- `設定ノード`

`設定ノード`の初期化処理の項目に以下を記述します。パーツ単体で動かす時は上書きし、他のパーツとセットで動かす時は上書きではなく追記しましょう。

```javascript
obnizParts.servo = obniz.wired("ServoMotor",{ signal:2 }); //サーボモーターをどのくらい回すかの信号を2番に設定
```

## 4. 結果

デプロイして実行し、`injectノード`のボタンを押すとサーボが1回だけ動きます。

## 5. 補足

サーボモータは角度を指定して動くので、次に動かす時は`changeノード`の数値を変えて実行してみましょう。
今回利用しているSG90というサーボモータは0~180度を指定してください。

■ 参考資料
[obnizの公式ドキュメント: ](https://docs.obniz.com/ja/sdk/parts/ServoMotor/README.md)