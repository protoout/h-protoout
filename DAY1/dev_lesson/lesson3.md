# Node-REDを使ってプログラムをつくってみよう

前のLessonでは、Obnizのパーツライブラリから簡易的にパーツを動作させる方法を学びました。

今度は、Node-RED上でObnizを操作し、

## 目標
Node-REDの基本的な操作がわかり、ObnizをNode-RED上で操作できるようになる

## やってみよう
引き続き、obnizでさまざまな電子部品を触っていきます。  
進行の都合上、時間次第で触らない部品が出てくる場合があります。あらかじめご了承ください。（その際は資料を参考にしながらご自身で進めていっていただきます）

## 【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意

<details>
<summary>【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意</summary>

- 極性に注意
  - 扱うセンサーやアクチュエーターは極性があるかないか（プラスマイナスの電流の向き）を注意しましょう。極性を間違えて配線をするとデバイスが熱を持って高温になったり、壊れたりする場合があります。
- 怪我注意
  - 扱い方を間違える怪我や火傷をする場合があります。注意レベルを上げましょう。
- 破損注意
  - 扱い方を間違えるとデバイスを壊す場合があります。注意レベルを上げましょう。
- プログラムを起動しっぱなしにしない
  - 別のセンサーやアクチュエーターを試す際は、 必ず一度`ctrl+c`でプログラムを停止させてから、付け替えるようにしましょう。
  - Node.jsのプログラムを起動したまま≒電気が通電しっぱなしの状態です。センサーなどがショートしてしまって破損や怪我に繋がる恐れがあります。
- 壊してしまった場合
  - obniz本体やパーツが熱くなっている場合があります。取り外す場合は注意しましょう。
  - 壊しても落ち込まずに！
    - たいてい誰でも1回は壊します。
    - パーツ自体はそれほど値段もしないので、勉強代と思っていきましょう。

</details>

## 基礎編②：目次

1. サーボモーター
2. 照度センサー（CdS）
3. 温度センサー
4. パトランプ

## 1. サーボモーター

<a href="https://gyazo.com/d0c9462e27bc17845f5a14bb81080897"><img src="https://i.gyazo.com/d0c9462e27bc17845f5a14bb81080897.jpg" alt="Image from Gyazo" width="700"/></a>

<a href="https://gyazo.com/6e51a64cd7b7ddbf16a7937a8561ee3a"><img src="https://i.gyazo.com/6e51a64cd7b7ddbf16a7937a8561ee3a.jpg" alt="Image from Gyazo" width="700"/></a>

小規模なIoTでもっともよく使われる「アクチュエーター」の1つです。  
通常のモーターは電流を流すと回転し続けますが、サーボモーターは特殊な電流を流すことで「軸の位相を任意の角度に変化」させることができます。

設定可能な最大角度・回転トルク（強さ）・設定角度の細かさなどは、サーボモーターの性能によって大きく変わってきます。  
今回扱うのはホビー用途でもっとも汎用的なモデルです。

### 1-1. obnizとの接続

[![Image from Gyazo](https://i.gyazo.com/9e761676b8bffafd044339fdc26199dc.jpg)](https://gyazo.com/9e761676b8bffafd044339fdc26199dc)

以下をまず準備してください。

- サーボモーター
- ジャンパワイヤ白1本
- ジャンパワイヤ赤1本
- ジャンパワイヤ青1本
- ブレッドボード

[![Image from Gyazo](https://i.gyazo.com/7569445e6968343962bec179da49a56c.jpg)](https://gyazo.com/7569445e6968343962bec179da49a56c)

最初はサーボモーターとジャンパワイヤを接続：

- サーボモーター茶 - ジャンパワイヤ白
- サーボモーター橙 - ジャンパワイヤ赤
- サーボモーター黄 - ジャンパワイヤ青

[![Image from Gyazo](https://i.gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461.png)](https://gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461)

[![Image from Gyazo](https://i.gyazo.com/78e42de894f9c2714afc006e27a0f521.png)](https://gyazo.com/78e42de894f9c2714afc006e27a0f521)

次にジャンパワイヤとobnizを接続：

- ジャンパワイヤ赤 - プラス
- ジャンパワイヤ白 - マイナス
- ジャンパワイヤ青 - obniz 2

このように接続できましたか？

最後に、回転してるかわかりやすいようにサーボにプラスチックパーツをつけましょう。（このパーツのことを**サーボホーン**といいます）  
好きな形状のもので構いません。

<a href="https://gyazo.com/c6cce3627ad4d4e6687e740d2fe2c27b"><img src="https://i.gyazo.com/c6cce3627ad4d4e6687e740d2fe2c27b.jpg" alt="Image from Gyazo" width="700"/></a>

### 1-2. ドキュメントページから実行

[![Image from Gyazo](https://i.gyazo.com/55e78fe8109fb6fc1aac86d150ed8a8e.gif)](https://gyazo.com/55e78fe8109fb6fc1aac86d150ed8a8e)

[部品を使う：サーボモーターを回す - obniz Docs](https://obniz.com/ja/doc/guides/obniz-starter-guide/parts-library/servo-motor)

上記にアクセスし、スクロールして一番下にあるサンプルでobniz IDを入力し、`実行`ボタンをクリックしてポップアップを開き、スライダーを動かすことでサーボモーターが連動して動くことを確認してください。

<details>
<summary>(補足)obniz Boardで過電流警告が出た場合の対策</summary>

[![Image from Gyazo](https://i.gyazo.com/87b44ab127c5f03b63ccce1b9eab71b1.png)](https://gyazo.com/87b44ab127c5f03b63ccce1b9eab71b1)

> **heavy output. output voltage is too low when driving high** が連続して発生することがあります。  
> 単純にこのスクリプトを再起動するか、ブレッドボードを経由して配線を行うかすると改善する場合があります。  
> ジャンパワイヤの抵抗値による過電流か、サーボモーターの個体差（相性）で発生する、ということが多いようです。

どうしても上記が発生してしまう場合は、

- ジャンパワイヤ（何色でもよい）2本
- ブレッドボード

を用意し、以下のように「もともと接続されていた赤いジャンパワイヤ」をobnizから取り外し、2本のジャンパワイヤを使ってブレッドボード上を経由させてobnizの1番ピンに接続してみてください。

[![Image from Gyazo](https://i.gyazo.com/1da8306c935fd4183c9d331a6cad8d0f.png)](https://gyazo.com/1da8306c935fd4183c9d331a6cad8d0f)

</details>

<details>
<summary>(補足)ハンチングについて</summary>

サーボモーターにはその構造上「ハンチング」という現象が起こります。  
これは特定の位置で停止した場合に、細かい振動を起こして完全には停止しない現象です。とくに0度や180度といった端点で発生することが多いため、以下のNode.jsでスクリプトを書くときなどは注意してください。  
（上記ドキュメントページのスライダーでも、一番端へ動かした場合に発生することがあります）
</details>

### 1-3. Node.jsで実行

<!-- [![Image from Gyazo](https://i.gyazo.com/b88f34195bd6883cc732431f49f13c6f.gif)](https://gyazo.com/b88f34195bd6883cc732431f49f13c6f) -->

`06_servo.js`を新規作成して以下のソースコードを貼り付け、Node.jsで動かしてみましょう。

```js:06_servo.js
const Obniz = require('obniz');
const obniz = new Obniz('Obniz_ID'); // Obniz_IDに自分のIDを入れます

obniz.onconnect = async function () {
  // サーボモータを利用
  const servo = obniz.wired('ServoMotor', { signal: 2 });

  // 角度を保持する変数
  let degrees = 90.0;

  // ディスプレイ表示（初期画面）
  obniz.display.clear();
  obniz.display.print('Hello obniz!');

  // スイッチの反応を常時監視
  // 「スイッチ状態が変化した瞬間に1回だけ実行される」ことに注意しましょう
  obniz.switch.onchange = function (state) {
    // スイッチの状態で角度を決め、最後に動かします
    if (state === 'push') {
      // スイッチが押されている状態
      console.log('pushed');
      degrees = 45.0;
    } else if (state === 'right') {
      // 右にスイッチを倒したとき
      console.log('right');
      degrees = 0.0;
    } else if (state === 'left') {
      // 左にスイッチを倒したとき
      console.log('left');
      degrees = 180.0;
    } else {
      // スイッチが押されていない状態
      console.log('released');
      degrees = 90.0;
    }
  
  // ディスプレイに角度を表示
  obniz.display.clear();
  obniz.display.print(`Current: ${degrees} deg`);
  // サーボを指定の角度まで動かします
  servo.angle(degrees);
  }
}
```

<details>
<summary>heavy output. output voltage is too low when driving highが発生する場合</summary>

[![Image from Gyazo](https://i.gyazo.com/c0c2cc772af37003785f5eb812225a09.png)](https://gyazo.com/c0c2cc772af37003785f5eb812225a09)
Node.jsでもこのような過電流警告が出ます。`Ctrl+C`でいったん終了させてから再度実行してみましょう。
</details>

## 2. 照度センサー（CdS） (🚨：火傷の危険があります。注意レベルを上げましょう)

![2019-06-20_19h27_25_result.jpg (441.4 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/07ce0f24-6b93-47ed-b668-9153aae9769d.jpg)

CdSといい、センサー部分にあたる光の強さによって抵抗値が変化します。  
（**可変抵抗素子**といいます）

通常の抵抗器（**固定抵抗素子**）と組み合わせることで、この「抵抗値の変化」を「電圧値の変化」として取り出すことができます。  
このセンサーはobnizのドキュメントにはありませんが、電子部品の発展編として実際に扱ってみます。

### 2-1. obnizとの接続

![2019-06-20_19h27_30_result.jpg (408.9 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/909d0f27-cd78-4386-9c6a-913114b1ae4b.jpg)

- CdS:1個
- 抵抗330Ω:1個
- ブレッドボード:1個
- ジャンパワイヤー赤:1本
- ジャンパワイヤー黒:1本
- ジャンパワイヤー白:1本

以上の6点の部品を準備してください。

[![Image from Gyazo](https://i.gyazo.com/aea0f2684723de82e05699203291fb76.png)](https://gyazo.com/aea0f2684723de82e05699203291fb76)

> 抵抗の数値は、カラーコードという色の帯で表現されています。
> 330Ωは `橙橙茶金` となります。  
> このあたりは[抵抗値早見表](http://part.freelab.jp/s_regi_list.html)などを参考にしてみてください。

(🚨：火傷の危険があります。注意レベルを上げましょう。)  
下記の回路をよく見て、接続を間違えないようにしましょう。

> CdSセルや抵抗が**含まれない**回路（ショート、短絡とも言います）があると、大量の電流が流れ高温になり、ブレッドボードが溶けたり、火傷の恐れがあります。

![2019-06-20_19h27_51_result.jpg (183.6 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/71cb5fbc-3f61-47e3-aaef-9da67ccc290e.jpg)

![2019-06-20_19h27_46_result.jpg (307.1 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg)

まずブレッドボードを横向き（横長方向）にし、CdSと抵抗を配置します。  
極性はありませんので方向は気にしなくてよいです。

次にジャンパワイヤ3本を写真のようにブレッドボードに挿し、さらに以下の通りにobnizと接続します。

- obniz 0 - ジャンパワイヤ赤
- obniz 1 - ジャンパワイヤ白
- obniz 2 - ジャンパワイヤ黒

![2019-06-20_19h27_58_result.jpg (298.9 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg)

### 2-2. 仕組み

[![Image from Gyazo](https://i.gyazo.com/d8f564c5f77f0608a31384faae4f9781.jpg)](https://gyazo.com/d8f564c5f77f0608a31384faae4f9781)

obnizの端子の機能を以下のように設定し、このうち1番端子の「電圧」を計測します。

- obniz 0 - 電圧出力（5V）
- obniz 1 - 電圧入力（CdSと抵抗の**分圧**）
- obniz 2 - 電圧出力（0V）

### 2-3. Node.jsで動かす

`07_cds.js`というファイルを新規作成し、以下のソースコードを動かしてみましょう。

```js:07_cds.js
const Obniz = require('obniz');
const obniz = new Obniz('obnizのデバイスID');

obniz.onconnect = async () => {
  obniz.io0.output(true);  // io0電圧を5Vに（電源＋）
  obniz.io2.output(false); // io2電圧を0Vに（電源−）

  // io1をアナログピンに(センサーの値を取得)
  obniz.ad1.start((voltage) => {
    // センサーの値が変わるたびに実行される
    console.log(`changed to ${voltage} v`);
  });
}
```

[![Image from Gyazo](https://i.gyazo.com/bd601bf2e7ad760a85064af9dc6ced4f.gif)](https://gyazo.com/bd601bf2e7ad760a85064af9dc6ced4f)

ここで使っている関数はCdS専用のものではなく、端子にかかっている電圧を測定して数値で表現できるような、汎用的なものとなります。  
obnizドキュメントにおいては  
[AD - obniz Docs](https://obniz.com/ja/doc/reference/common/ad)  
がこの関数に対応したページとなります。

> 参考：[obnizとNode.jsでCdSセル(照度センサ)を使ってみる](https://zenn.dev/protoout/articles/01-obniz-nodejs-cds)

---

その他、obnizで公式に動作確認・サポートされているパーツは、[obnizパーツライブラリ](https://docs.obniz.com/ja/sdk/parts)から参照できます。

この中にないものを触ってみたい場合も動かせる可能性はありますが、まずはパーツライブラリから選ぶのが手っ取り早くてオススメです。

### 3. 温湿度センサー



### 4. パトランプ

```JSON
[{"id":"871663456440f96f","type":"obniz-function","z":"922cab1da68a7d27","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.light.single(msg.payload);\n\nreturn msg;","x":520,"y":640,"wires":[["d71cc6845528f6b3"]]},{"id":"daafa2b76adf4485","type":"inject","z":"922cab1da68a7d27","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"red","payloadType":"str","x":230,"y":560,"wires":[["871663456440f96f"]]},{"id":"08057ff0788ce9fd","type":"inject","z":"922cab1da68a7d27","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"green","payloadType":"str","x":230,"y":660,"wires":[["871663456440f96f"]]},{"id":"d71cc6845528f6b3","type":"debug","z":"922cab1da68a7d27","name":"debug 3","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":760,"y":640,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"","accessToken":"","code":"obniz.display.clear(); // 画面を消去\nobnizParts.light = obniz.wired(\"Keyestudio_TrafficLight\", { gnd: 0, green: 1, yellow: 2, red: 3 });"}]

```




