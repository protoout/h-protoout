# 超音波測距センサーで距離を取得しよう

### **新しいことをはじめる前に**  

[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。

---

## 1.やってみよう

<a href="https://gyazo.com/fb6794ca04c3dc04461f6816300ee107"><img src="https://i.gyazo.com/fb6794ca04c3dc04461f6816300ee107.jpg" alt="Image from Gyazo" width="500"/></a>

<a href="https://gyazo.com/7fadb5f3af05b39938f81b059a6f81fd"><img src="https://i.gyazo.com/7fadb5f3af05b39938f81b059a6f81fd.jpg" alt="Image from Gyazo" width="500"/></a>

超音波を発生し、物体に当たってから跳ね返ってくるまでの時間を計測することで、その対象物体との距離を算出できます。  
距離を測るだけでなく、単純に目の前に人がいるかいないか、といった用途にも使えます。

### 1-1. obnizとの接続

<a href="https://i.gyazo.com/5aaa82526f0dc855ad47bc2916925506"><img src="https://i.gyazo.com/5aaa82526f0dc855ad47bc2916925506.jpg" alt="Image from Gyazo" width="500"/></a>

写真のように、超音波測距センサーをこちら側に向けた状態でobnizの左端に寄せて4つの端子をすべて差し込みます。obniz端子との対応は以下の通りとなっているので、念のため確認してください。

- obniz 0 - 超音波Gnd
- obniz 1 - 超音波Echo
- obniz 2 - 超音波Trig
- obniz 3 - 超音波Vcc

### 1-2. obnizの公式ページから動作を確認する

その他のセンサーと同様に、以下リンクよりドキュメントページにアクセスし、`[await] measureWait()` と書かれているサンプルを実行してみましょう。

[HC-SR04 | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/HC-SR04/README.md)

<img src="https://i.gyazo.com/68b8327f55c08edd1ef968a7d4d6cf2c.png" alt="Image from Gyazo" width="500"/>

<img src="https://i.gyazo.com/769140216591bfcf8bcea87f816e0986.gif" alt="Image from Gyazo" width="500"/>


### 1-3. Node.jsで実行


<a href="https://gyazo.com/9a751daa7ef2e9f48a710826476781c0"><img src="https://i.gyazo.com/9a751daa7ef2e9f48a710826476781c0.png" alt="Image from Gyazo" width="500"/></a>


下記のフローを読み込み、初期化処理コードを書き換えてください。
```json
[{"id":"e42d3d96.12046","type":"obniz-repeat","z":"35131428dc29ef13","obniz":"","name":"","interval":"1000","code":"msg.payload = await obnizParts.hcsr04.measureWait();\n\nreturn msg;","x":250,"y":300,"wires":[["0f3f684d5bf465a7"]]},{"id":"402408dd.31b188","type":"debug","z":"35131428dc29ef13","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":810,"y":300,"wires":[]},{"id":"0f3f684d5bf465a7","type":"template","z":"35131428dc29ef13","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"距離は: {{payload}} ","output":"str","x":540,"y":300,"wires":[["402408dd.31b188"]]}]
```


▼初期化処理コード
```json

obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 });

```


## 2.演習

### 2-1. templateノードの中身を書き換えて、単位をつけよう

templateノードは、前のノードから渡されたデータを任意のテンプレートに入れて出力するものです。

設定を変えて、数字のデータでなく「mm」をつけて出力するように書き換えてみましょう。


ヒント: [templateノードについて](../lesson02-node-red-basic/01_node-red-corenode.md)を使います。


### 2-2.【応用】 50mm以下になったらコンソールに「近すぎる！」と出力されるものを作ってみましょう。

ヒント: [switchノードとchangeノード](../lesson02-node-red-basic/01_node-red-corenode.md)を使います。

---

**[◀ 目次ページに戻る](../readme.md)**