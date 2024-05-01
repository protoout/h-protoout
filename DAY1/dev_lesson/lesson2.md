# Obnizで、LEDやセンサーを試してみよう

## 目標
obnizの基本的な使い方を学ぶ

 - **インジケータ**(対象の状態を標示する装置)によって、情報を表示・通知する。: LED
  - **センサ**によって、光や温度といった環境情報を取得したり、変化を検知したりする。: 超音波距離センサ
  - **アクチュエータ**（動力源と機構部品を組み合わせて機械的な動作を行う装置）によって、実際のモノを動かす。: サーボモーター
 

Obnizが提供するパーツライブラリを使って、簡単に動作を試すことができます。
ひとつひとつ試していきましょう！

## やってみよう

## 【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意
- **配線のときは必ず電源を抜くこと！**
- 配線は図をしっかり見て間違えがないか確認をしてから最後にUSBケーブルをさして電源を供給しましょう。
- 極性に注意
  - 扱うセンサーやアクチュエーターは極性があるかないか（プラスマイナスの電流の向き）を注意しましょう。極性を間違えて配線をするとデバイスが熱を持って高温になったり、壊れたりする場合があります。
- 怪我注意
  - 扱い方を間違える怪我や火傷をする場合があります。注意レベルを上げましょう。
- 破損注意
  - 扱い方を間違えるとデバイスを壊す場合があります。注意レベルを上げましょう。
- 壊してしまった場合
  - obniz本体やパーツが熱くなっている場合があります。取り外す場合は注意しましょう。
  - 壊しても落ち込まずに！
  - たいてい誰でも1回は壊します。
  - パーツ自体はそれほど値段もしないので、勉強代と思っていきましょう。
- プログラムを起動しっぱなしにしない
  - Node.jsのプログラムを起動したまま≒電気が通電しっぱなしの状態です。センサーなどがショートしてしまって破損や怪我に繋がる恐れがあります。
  - 別のセンサーやアクチュエーターを試す際は、 必ず一度`ctrl+c`でプログラムを停止させてから、付け替えるようにしましょう。
  - 新たなプログラムを起動する際は、毎回必ずobnizディスプレイにQRコードとobniz IDが表示されていることを確認してください。

## 基礎編①：目次

1. 開発準備
2. Lチカ
6. 超音波測距センサー
2. スピーカー

## 1. 開発準備

**obniz IDを（手元に）メモしておきましょう！**

### 1-1 Node-REDにobnizノードをインストール
1. Node-REDにログインしてください。

2. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

3. 「ノードを追加」をクリックし「obniz」で検索してください。
   
   検索結果から`node-red-contrib-obniz`の「ノードを追加」を押してください。  
   （vnがついて**いない**方です！）
   
   <a href="https://gyazo.com/44977736c5df5749bfeb4102fc7e1d37"><img src="https://i.gyazo.com/44977736c5df5749bfeb4102fc7e1d37.png" alt="Image from Gyazo" width="800"/></a>

4. Node-REDの左側の「その他」の中に青いobnizノードが表示されていれば準備完了です。
   
   <a href="https://gyazo.com/1dc3e137af72509caed03e378f2861e3"><img src="https://i.gyazo.com/1dc3e137af72509caed03e378f2861e3.png" alt="Image from Gyazo" width="166"/></a>

obnizのノードはこんなときに使います。
- obniz repeat・・・常にデータを取り続けたいとき  
  例）温度センサー、距離センサー、照度センサーなどのセンサが検知したデータを一定間隔で取得し続ける、など。  

- obniz function・・・フロー上のきっかけでなにか動作させたいとき  
  例）LINE Botが受け取ったメッセージをきっかけに温度を取得する、など。

参考ページ：[Node-REDのobnizノードがバージョンアップした！](https://qiita.com/wicket/items/e150e78cd787da03493e)

### 1-2 処理停止用ノードを読み込む

Node-RED上で起動しているobnizのプログラムを止めるためには、obnizのcloseメソッドを明示的に実行する必要があります。  
なので、作業に入る前に処理停止用のノードを作成しておきましょう。  
今回は事前に作成したものをJSON形式で書き出しておきました。  
以下の手順で自身のNode-RED上に読み込みを行ってください。  

JSONコードの読み込みは第1回授業の復習です。思い出してやってみましょう。

1. 下記のコードをすべてコピーしてください。

```json
[{"id":"cb1d6d3a.017e1","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":610,"y":140,"wires":[]},{"id":"11a346f0.5a4c19","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"msg.payload = \"finish\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":440,"y":140,"wires":[["cb1d6d3a.017e1"]]},{"id":"76e43759.3dff68","type":"inject","z":"d9dba4a1.01f228","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":260,"y":140,"wires":[["11a346f0.5a4c19"]]}]
```

▼読み込み結果  
<a href="https://gyazo.com/ac38f368a5f4fefc730b30c4b6984944"><img src="https://i.gyazo.com/ac38f368a5f4fefc730b30c4b6984944.png" alt="Image from Gyazo" width="579"/></a>

1. `obniz function` ノードをダブルクリックで開き、プロパティの「新規に obniz を追加…」の右に表示されている鉛筆マークを押下してください。
   
   <a href="https://gyazo.com/99f8fac66fc13afb07562d3fecdfcfdf"><img src="https://i.gyazo.com/99f8fac66fc13afb07562d3fecdfcfdf.png" alt="Image from Gyazo" width="627"/></a>

2. 表示されたプロパティ画面で、以下のとおり設定し「追加」を押下してください。  
   - obniz ID：自分のobniz ID  
   - device type：obnizBoard 1Y
   - 初期化処理：以下コード  
   
   ```javascript
   obniz.display.clear(); // 画面を消去
   ```
   
   <a href="https://gyazo.com/5a850defef827a60867cf1af4194029d"><img src="https://i.gyazo.com/5a850defef827a60867cf1af4194029d.png" alt="Image from Gyazo" width="634"/></a>

3. obniz-functionノードを編集のプロパティ画面に戻ったら、「obniz」に前工程で設定したobniz IDが設定されていることを確認し、「完了」を押下してください。
   
   <a href="https://gyazo.com/593d9ee6524567b902dde5a842a46745"><img src="https://i.gyazo.com/593d9ee6524567b902dde5a842a46745.png" alt="Image from Gyazo" width="649"/></a>

【見てみよう】  
`obniz function`ノードをもう一度開き、中身を見てみましょう。  
コードの内容は以下のとおりとなっています。  
（実際のコードにはコメントはつけていません。）  

```javascript
msg.payload = "finish"; //msg.payloadに"finish"を格納→debugに"finish"と表示されます
await obniz.wait(1000); //1000ミリ秒＝1秒obnizの処理を待機 
obniz.close(); //意図的にclose()関数を呼ぶことで通信を切断

return msg;
```

このように、Node-REDでobnizを使用する場合、ノードの中にコードを書く必要があります。  
これ以降に読み込むノードにも同じようにコードが設定されていますので、  
JSONコードを読み込んだ後にそれぞれのノードを開いてコードを確認してみてください。  


**※注意※**  
- 以降の作業でノードを読み込む前に、処理停止用のノード**以外は**削除するようにしてください。  
  ノードが混在すると分かりづらくなるのと、obnizが予期せぬ動作をすることがあるためです。
- 不要なobniz IDの設定を削除する場合、「初期化処理」の内容も削除されますので注意してください。  
  「初期化処理」のコードを残しておきたい場合は、obniz IDの設定を削除する前にコードをコピーしメモ帳等に退避しておくようにしましょう。  
  
  <a href="https://gyazo.com/be2c84ffa92899c86b7e03fc2b49f8ec"><img src="https://i.gyazo.com/be2c84ffa92899c86b7e03fc2b49f8ec.png" alt="Image from Gyazo" width="742"/></a>
  <a href="https://gyazo.com/f143836702081d6960800f4668aef7be"><img src="https://i.gyazo.com/f143836702081d6960800f4668aef7be.png" alt="Image from Gyazo" width="648"/></a>


## 2. Lチカしてみよう

<a href="https://gyazo.com/23a5a24bdd5a812ed8baf83ced57b590"><img src="https://i.gyazo.com/23a5a24bdd5a812ed8baf83ced57b590.jpg" alt="Image from Gyazo" width="700"/></a>


> ソフトウェアの世界では一番最初に書く最も簡単なコードのことを「Hello World」と言いますが、ハードウェアの世界ではLEDを点滅させる「**Lチカ**」がそれに相当します。

<details>
<summary>(補足)LEDと抵抗の切っても切れない関係</summary>

[![Image from Gyazo](https://i.gyazo.com/4affed7a9a893c86880d9ff974562cf4.jpg)](https://gyazo.com/4affed7a9a893c86880d9ff974562cf4)

[![Image from Gyazo](https://i.gyazo.com/1e31004da05e837a9c631917b606c27e.png)](https://gyazo.com/1e31004da05e837a9c631917b606c27e)

本来、LEDは必ず抵抗とセットで使うのが電子工作における決まりごとになっていますが、今回は抵抗が内蔵されたLEDを利用するため、これ1つを直接obnizに接続することで制御ができます。
</details>

### 2-1. まずは光らせてみよう

[![Image from Gyazo](https://i.gyazo.com/4bb4d4af379c881b0f68274869c18505.png)](https://gyazo.com/4bb4d4af379c881b0f68274869c18505)

脚の長いほうがアノード、短いほうをカソードといいます。  

obnizに電源が入っている状態で、写真のように  

- LEDの長い脚（アノード）をobnizの＋端子
- LEDの短い脚（カソード）をobnizの－端子

に接続してみてください。光りましたか？

> - 光らない場合は、以下を確認しましょう。
>   - 脚が逆になっていないか
>   - 3つある穴の中央に挿していないか（両脇の穴を使ってください）

obnizのプラス端子とマイナス端子を繋ぐことで通電し、LEDが光るようになります。

### 2-2. obnizで制御できるように接続

[![Image from Gyazo](https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png)](https://gyazo.com/72603bdeeae78020b1a3625f06044b6d)

- LEDの長い脚をobnizの0番
- LEDの短い脚をobnizの1番

に接続してください。

### 2-3. ドキュメントページから実行

obniz公式のドキュメントから実行してみましょう。  
以下のリンクにアクセスしてください。

[LED | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

このドキュメントページの中の `on` と書かれているサンプルを探し、自分のobniz IDを入力して `実行` をクリックしてみましょう。

[![Image from Gyazo](https://i.gyazo.com/eeec7fc6bb18ee0ff4767e8d6d1d2946.png)](https://gyazo.com/eeec7fc6bb18ee0ff4767e8d6d1d2946)

実行後は右上の`終了`ボタンで処理を止めておきます。  
Node.jsでいう`Ctrl + C`と同じです。

<a href="https://gyazo.com/f4015ac1a321312a399818c810063ee5"><img src="https://i.gyazo.com/f4015ac1a321312a399818c810063ee5.png" alt="Image from Gyazo" width="1027"/></a>

`off`や`blink`なども実行してみましょう！

#### 2-3-1. ドキュメントから実行できるのはLEDだけじゃないです

obnizの公式オンラインドキュメントには「[obniz Parts Library](https://docs.obniz.com/ja/sdk/parts)」というものがあります。  
ここに掲載されている電子部品であれば、

1. ドキュメントの指示通りに接続  
2. 自分のobniz IDを入力  
3. `実行`をクリック  
のわずか3ステップで動作確認を行うことができます。便利！

新しい電子部品を自分で使ってみるときは、まずこの「obniz Parts Library」に使いたい電子部品と同じか、似たようなものがないかを調べ、できるだけ対応した（掲載されている）部品を使うようにするとすぐに動作確認ができるのでオススメです。

また、この「obniz Parts Library」で動作しているのは**Node.jsではなく通常のブラウザ版JavaScript**です。  
「**Webブラウザからもobnizが扱える**」ことをぜひ覚えておいてください。
<!-- （のちの授業で扱っていきます！） -->

### 2-4. Node-REDで実行

<a href="https://gyazo.com/17852495dc721319ae13da119fa852d7"><img src="https://i.gyazo.com/17852495dc721319ae13da119fa852d7.gif" alt="Image from Gyazo" width="646"/></a>

以下のソースコードを読み込み、Node-REDで動かしてみましょう。  
obnizのスイッチを押すとLEDが点灯するのを確認してください。  
ノードの中身は各自で確認してみてください。  

```json
[{"id":"5fa9057f.f2e0ac","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nreturn msg;","x":330,"y":340,"wires":[["ebafa559.00b978","e8f7976.0477568"]]},{"id":"ebafa559.00b978","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"obniz.display.clear(); // 画面を消去\r\n\r\nif (msg.payload === 'push') {\r\n // スイッチが押されている状態\r\n obniz.display.print('LED ON');\r\n obnizParts.led.on();\r\n} else {\r\n // スイッチが押されていない状態\r\n obniz.display.print('LED OFF');\r\n obnizParts.led.off();\r\n}\r\n","x":520,"y":340,"wires":[[]]},{"id":"e8f7976.0477568","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":510,"y":420,"wires":[]}]
```
▼読み込み結果  
<a href="https://gyazo.com/cccec7050a56c2e266600819460d4694"><img src="https://i.gyazo.com/cccec7050a56c2e266600819460d4694.png" alt="Image from Gyazo" width="374"/></a>  

▼初期化処理コード  
```javascript
obniz.display.clear(); // 画面を消去
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 });
```

2-5. やってみよう

### 3-1. 完成イメージ

[![Image from Gyazo](https://i.gyazo.com/57d085bc072e86acc5391d4d88beeaee.gif)](https://gyazo.com/57d085bc072e86acc5391d4d88beeaee)

### 3-2. 使い方ドキュメント

詳細な使い方が載っています。後にご自身で確認しておいてください。

- [スイッチ \- obniz Docs](https://docs.docs.obniz.com/ja/guides/common/switch/)
- [Display \- obniz Docs](https://docs.docs.obniz.com/ja/guides/common/display/)

### 3-3. ソースコードを実行する

`02_switch_display.js`というファイルを作成し、  
次のソースコードを貼り付けていったん保存してください。

```js:02_switch_display.js
const Obniz = require('obniz');
const obniz = new Obniz('Obniz_ID');  // Obniz_IDに自分のIDを入れてください

// obnizがオンラインであることが確認されたら、以下の関数内が自動で実行されます
obniz.onconnect = async function () {
  obniz.display.clear(); // 画面を消去
  obniz.display.print('Hello obniz!');  // Hello obniz! と画面に表示

  // スイッチの反応を常時監視、変化があれば実行します
  obniz.switch.onchange = function (state) {
    if (state === 'push') {
      // 押されたとき
      console.log('pushed');
      obniz.display.clear(); // 画面を消去
      obniz.display.print('pushed');  // pushed と画面に表示
    } else if (state === 'right') {
      // 右にスイッチを倒したとき（やさしく）
      console.log('pressed right');
      obniz.display.clear(); // 画面を消去
      obniz.display.print('pressed right');  // pressed right と画面に表示
    } else if (state === 'left') {
      // 左にスイッチを倒したとき（やさしく）
      console.log('pressed left');
      obniz.display.clear(); // 画面を消去
      obniz.display.print('pressed left');  // pressed left と画面に表示
    }
  }
}
```

保存できましたら、2行目に自分のobniz IDに書き換え、再度保存してからNode.jsで実行してみましょう。

```bash
node 02_switch_display.js
```

画面に`Hello obniz!`と表示されたら、スイッチをいろいろと動かしてみましょう。  
`obniz.display ...` はobnizのディスプレイへの表示を行う関数で、  
`console.log()` はターミナル上への表示を行う関数です。



## 5. スピーカー

<a href="https://gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57"><img src="https://i.gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57.jpg" alt="Image from Gyazo" width="700"/></a>

任意の高さの音を出すことができるスピーカーです。  
「インジケーター」の1つで、これ1つでブザーやアラームといった通知系デバイスを作ることができます。

保護紙をつまんでまっすぐスピーカーを引っ張ると抜き取ることができます。  

### 5-1. obnizとの接続

<a href="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf"><img src="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf.jpg" alt="Image from Gyazo" width="700"/></a>

obnizの0番と1番の端子に差し込みます。  
極性（方向）はなく、どちらの向きで差し込んでも大丈夫です。

### 5-2. ドキュメントページから実行

次は先に、obnizの公式ドキュメントからサンプルを実行してみましょう。  
温度センサーのときを思い出しながら、以下のリンクにアクセスして音を鳴らしてみてください。  
サンプルは `play(frequency)` と書かれている場所のものを使いましょう。

[Speaker | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/Speaker/README.md)

![image.png (51.5 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/3641c01c-67aa-4150-8074-b4c949fd16c7.png)

サンプルは、ブラウザ上で直接コードを書き換えることができます。  
1000Hzと書いてある部分を、500や1500など好きな値に変更して再実行し、音が変化していることを確認してください。  
参考：[音階周波数](https://tomari.org/main/java/oto.html)

> 音楽好きであれば、これ1つで楽器を作るのも楽しいかもしれません！

### 5-3. Node.jsで実行

`04_speaker.js`を新規作成して以下のソースコードを貼り付け、Node.jsで動かしてみましょう。

```js:04_speaker.js
const Obniz = require('obniz');
const obniz = new Obniz('Obniz_ID'); // Obniz_IDに自分のIDを入れます

obniz.onconnect = async function () {
  // スピーカーを利用
  const speaker = obniz.wired('Speaker', { signal: 0, gnd: 1 });

  // ディスプレイ表示
  obniz.display.clear();
  obniz.display.print('Speaker test');

  // スイッチの反応を常時監視
  // 「スイッチ状態が変化した瞬間に1回だけ実行される」ことに注意しましょう
  obniz.switch.onchange = function (state) {
    if (state === 'push') {
      // スイッチが押されている状態
      obniz.display.clear();
      obniz.display.print('beep!');
      // 1000Hz で音を鳴らす
      speaker.play(1000);
    } else if (state === 'none') {
      // スイッチが押されていない状態
      obniz.display.clear();
      obniz.display.print('silent');
      // 音を停止する
      speaker.stop();
    }
  }
}
```

スイッチを押したり離したりして、スピーカーのコントロールができます。

### 5-4. おまけ

#### 5-4-1. 時報

```js
const Obniz = require('obniz');
const { exit } = require('process');
const obniz = new Obniz('Obniz_ID'); // Obniz_IDに自分のIDを入れます

// 任意の秒数待つことができる関数
// 参考: https://qiita.com/suin/items/99aa8641d06b5f819656
const sleep = (msec) => new Promise(res => setTimeout(res, msec));

// obnizが接続済み
obniz.onconnect = async function () {
  // スピーカーを利用
  const speaker = obniz.wired('Speaker', { signal: 0, gnd: 1 });

  // ﾎﾟｯ↓
  speaker.play(500); await sleep(300); speaker.stop(); await sleep(700);
  // ﾎﾟｯ↓
  speaker.play(500); await sleep(300); speaker.stop(); await sleep(700);
  // ﾎﾟｯ↓
  speaker.play(500); await sleep(300); speaker.stop(); await sleep(700);
  // ﾎﾟ~~~ﾝ↑
  speaker.play(1000); await sleep(1000); speaker.stop();
  // Ctrl+C を打たなくても自動で終了します
  exit();
}
```

#### 5-4-2. 半音ずつ音階を指定して音を鳴らす

```js
const Obniz = require('obniz');
const obniz = new Obniz('Obniz_ID'); // Obniz_IDに自分のIDを入れます

// MIDIノート番号から実際の周波数に変換する
function getFrequency(note_number) {
  // http://www.asahi-net.or.jp/~HB9T-KTD/music/Japan/Research/DTM/freq_map.html
  return Math.round(440 * (2 ** ((note_number - 69) / 12)));
}

// obnizが接続済み
obniz.onconnect = async function () {
  // スピーカーを利用
  const speaker = obniz.wired('Speaker', { signal: 0, gnd: 1 });
  // MIDIノート番号
  let noteNumber = 72;
  // 現在の周波数
  let freq = 523;

  // ディスプレイ表示
  obniz.display.clear();
  obniz.display.print('Musical Scale');

  // スイッチの反応を常時監視
  obniz.switch.onchange = function (state) {
    // 画面クリア
    obniz.display.clear();

    if (state === 'push') {
      // スイッチが押されている状態
      speaker.play(freq); // 音を鳴らす
    } else if (state === 'right') {
      // 右にスイッチを倒したとき
      if (noteNumber < 127) noteNumber++; // ノート番号+1
      freq = getFrequency(noteNumber); // 周波数を再計算
    } else if (state === 'left') {
      // 左にスイッチを倒したとき
      if (noteNumber > 0) noteNumber--; // ノート番号-1
      freq = getFrequency(noteNumber); // 周波数を再計算
    } else {
      // スイッチが押されていない状態
      speaker.stop(); // 音を停止する
    }

    // 現在の周波数を表示
    obniz.display.print(freq);
  }
}
```

## 6. 超音波測距センサー

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