# スピーカーで音を鳴らしてみよう

**※注意※**  
- 以降の作業でノードを読み込む前に、Node-REDの**タブを無効化**し、有効なタブは常に1つのみにしてください。ノードが混在すると分かりづらくなるのと、obnizが予期せぬ動作をすることがあるためです。


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

