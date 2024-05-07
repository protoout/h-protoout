# 超音波測距センサーで距離を取得しよう


### **新しいことをはじめる前に※**  

1つページが終わり次のことをはじめる前に、下記3つの手順をかならず行うようにしてください

**1. タブの無効化**

以降の作業でノードを読み込む前に、今まで作業していたNode-REDの**タブを無効化**し、有効なタブは必ず常に1つのみにしてください。
ノードが混在すると分かりづらくなりobnizが予期せぬ動作をすることがあります。

<img src="https://i.gyazo.com/48f43c4c3ea95f30a4569f382490cc05.png" width="500">

**2. タブの新規作成**
1. 「+」をクリック
<a href="https://gyazo.com/6a6d96fec786b923f70512e1de4b3551"><img src="https://i.gyazo.com/6a6d96fec786b923f70512e1de4b3551.png" alt="Image from Gyazo" width="500"/></a>

2. 新しくできたタブをダブルクリックし、名前をわかりやすく変更する。
<a href="https://gyazo.com/9392ad19397802dbfb49f53550cc48f5"><img src="https://i.gyazo.com/9392ad19397802dbfb49f53550cc48f5.png" alt="Image from Gyazo" width="500"/></a>

**3. 停止用フローの読み込み**
1. 下記のコードをすべてコピーしてください。

```json
[{"id":"cb1d6d3a.017e1","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":610,"y":140,"wires":[]},{"id":"11a346f0.5a4c19","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"msg.payload = \"close\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":440,"y":140,"wires":[["cb1d6d3a.017e1"]]},{"id":"76e43759.3dff68","type":"inject","z":"d9dba4a1.01f228","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":260,"y":140,"wires":[["11a346f0.5a4c19"]]}]
```

Node-REDの右上のメニュー（三本線）から読み込みを選びます。

<a href="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c"><img src="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c.png" alt="Image from Gyazo" width="372"/></a>

      

コピーしたコードを貼り付けます  
<a href="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a"><img src="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a.png" alt="Image from Gyazo" width="372"/></a>


---

## やってみよう

<a href="https://gyazo.com/fb6794ca04c3dc04461f6816300ee107"><img src="https://i.gyazo.com/fb6794ca04c3dc04461f6816300ee107.jpg" alt="Image from Gyazo" width="700"/></a>

<a href="https://gyazo.com/7fadb5f3af05b39938f81b059a6f81fd"><img src="https://i.gyazo.com/7fadb5f3af05b39938f81b059a6f81fd.jpg" alt="Image from Gyazo" width="700"/></a>

超音波を発生し、物体に当たってから跳ね返ってくるまでの時間を計測することで、その対象物体との距離を算出できます。  
距離を測るだけでなく、単純に目の前に人がいるかいないか、といった用途にも使えます。

### 6-1. obnizとの接続

<a href="https://i.gyazo.com/5aaa82526f0dc855ad47bc2916925506"><img src="https://i.gyazo.com/5aaa82526f0dc855ad47bc2916925506.jpg" alt="Image from Gyazo" width="700"/></a>

写真のように、超音波測距センサーをこちら側に向けた状態でobnizの左端に寄せて4つの端子をすべて差し込みます。obniz端子との対応は以下の通りとなっているので、念のため確認してください。

- obniz 0 - 超音波Gnd
- obniz 1 - 超音波Echo
- obniz 2 - 超音波Trig
- obniz 3 - 超音波Vcc

### 6-2. ドキュメントページから実行

その他のセンサーと同様に、以下リンクよりドキュメントページにアクセスし、`[await] measureWait()` と書かれているサンプルを実行してみましょう。

[HC-SR04 | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/HC-SR04/README.md)

[![Image from Gyazo](https://i.gyazo.com/68b8327f55c08edd1ef968a7d4d6cf2c.png)](https://gyazo.com/68b8327f55c08edd1ef968a7d4d6cf2c)

[![Image from Gyazo](https://i.gyazo.com/769140216591bfcf8bcea87f816e0986.gif)](https://gyazo.com/769140216591bfcf8bcea87f816e0986)

### 6-3. Node.jsで実行

[![Image from Gyazo](https://i.gyazo.com/07a7c83226d87860b3f260548f8dc7b0.gif)](https://gyazo.com/07a7c83226d87860b3f260548f8dc7b0)

以下のフローを読み込み、初期化処理フローを設定し動かしてみましょう。
デバッグに距離が出力され、50mm以下になったらobnizaディスプレイに「Too close!!」と出力されることを確認してみましょう。

```json
[{"id":"e42d3d96.12046","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"1000","code":"msg.payload = await obnizParts.hcsr04.measureWait();\n\nobniz.display.clear(); // クリア\nobniz.display.print('Ready');\n\n// 距離を取得\nlet distance = msg.payload;\n// そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい\ndistance = Math.floor(distance);\n\n// 距離(mm)をデバッグに表示\nmsg.payload = (distance + ' mm');\n// obnizディスプレイに表示\n// 一度消してから距離+mmの単位を表示\nobniz.display.clear();\nobniz.display.print(distance + ' mm');\n\n// 距離がある程度未満かどうかの判定\nif (distance < 50) { // 50mm = 5cm 以下の場合\n    // obnizディスプレイに近接していることを表示\n    obniz.display.clear();\n    obniz.display.print('Too close!!');\n}\n\nreturn msg;","x":310,"y":300,"wires":[["402408dd.31b188"]]},{"id":"402408dd.31b188","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":490,"y":300,"wires":[]}]
```

▼初期化処理フロー
```json
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 });
```


## まとめ
obnizの基本的な使い方がわかりました！


でも、今はまだ、それぞれ1つずつ動かしただけ。


センサーの状態によってLEDの光らせ方を変えたり、サーボモーターを動かしたりしたいですよね？


次のLessonではNode-REDを使って、連携させていきます！

---

**[◀ 目次ページに戻る](../readme.md)**