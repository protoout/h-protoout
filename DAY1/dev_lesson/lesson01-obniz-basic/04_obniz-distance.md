# 超音波測距センサーで距離を取得しよう

**※注意※**  
- 以降の作業でノードを読み込む前に、Node-REDの**タブを無効化**し、有効なタブは常に1つのみにしてください。ノードが混在すると分かりづらくなるのと、obnizが予期せぬ動作をすることがあるためです。


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

以下のソースコードを読み込み、初期化処理コードを設定し動かしてみましょう。
デバッグに距離が出力され、50mm以下になったらobnizaディスプレイに「Too close!!」と出力されることを確認してみましょう。

```json
[{"id":"e42d3d96.12046","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"1000","code":"msg.payload = await obnizParts.hcsr04.measureWait();\n\nobniz.display.clear(); // クリア\nobniz.display.print('Ready');\n\n// 距離を取得\nlet distance = msg.payload;\n// そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい\ndistance = Math.floor(distance);\n\n// 距離(mm)をデバッグに表示\nmsg.payload = (distance + ' mm');\n// obnizディスプレイに表示\n// 一度消してから距離+mmの単位を表示\nobniz.display.clear();\nobniz.display.print(distance + ' mm');\n\n// 距離がある程度未満かどうかの判定\nif (distance < 50) { // 50mm = 5cm 以下の場合\n    // obnizディスプレイに近接していることを表示\n    obniz.display.clear();\n    obniz.display.print('Too close!!');\n}\n\nreturn msg;","x":310,"y":300,"wires":[["402408dd.31b188"]]},{"id":"402408dd.31b188","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":490,"y":300,"wires":[]}]
```

▼初期化処理コード
```json
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 });
```


## まとめ
Obnizの基本的な使い方がわかりました！


でも、今はまだ、それぞれ1つずつ動かしただけ。


センサーの状態によってLEDの光らせ方を変えたり、サーボモーターを動かしたりしたいですよね？


次のLessonではNode-REDを使って、連携させていきます！