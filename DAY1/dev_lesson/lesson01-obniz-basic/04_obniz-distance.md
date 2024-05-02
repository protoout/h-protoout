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

`05_ultrarange.js`というファイルを新規作成し、以下のソースコードを動かしてみましょう。

```js:05_ultrarange.js
const Obniz = require('obniz');
const obniz = new Obniz('Obniz_ID'); // Obniz_IDに自分のIDを入れます

obniz.onconnect = async function () {
  // 超音波測距センサを利用する
  const hcsr04 = obniz.wired('HC-SR04', { gnd: 0, echo: 1, trigger: 2, vcc: 3 });

  // ディスプレイ
  obniz.display.clear(); // クリア
  obniz.display.print('Hello obniz!');
  //obniz.display.print('Hello obniz!'); // Hello obniz! と表示

  // setIntervalで一定間隔で処理
  setInterval(async function () {
    // 距離を取得
    let distance = await hcsr04.measureWait();
    // そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい
    //distance = Math.floor(distance);

    // 距離(mm)をターミナルに表示
    console.log(distance + ' mm');
    // obnizディスプレイに表示
    // 一度消してから距離+mmの単位を表示
    obniz.display.clear();
    obniz.display.print(distance + ' mm');

    // 距離がある程度未満かどうかの判定
    if (distance < 50) { // 50mm = 5cm 以下の場合
      // obnizディスプレイに近接していることを表示
      obniz.display.clear();
      obniz.display.print('Too close!!');
    }
  }, 1000); // 1000ミリ秒 = 1秒おきに実行
}
```


## まとめ
Obnizの基本的な使い方がわかりました！


でも、今はまだ、それぞれ1つずつ動かしただけ。


センサーの状態によってLEDの光らせ方を変えたり、サーボモーターを動かしたりしたいですよね？


次のLessonではNode-REDを使って、連携させていきます！