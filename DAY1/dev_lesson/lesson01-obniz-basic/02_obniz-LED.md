# Lチカしてみよう

**※注意※**  
- 以降の作業でノードを読み込む前に、Node-REDの**タブを無効化**し、有効なタブは常に1つのみにしてください。ノードが混在すると分かりづらくなるのと、obnizが予期せぬ動作をすることがあるためです。


<img src="https://i.gyazo.com/23a5a24bdd5a812ed8baf83ced57b590.jpg" alt="Image from Gyazo" width="700"/>

ソフトウェアの世界では一番最初に書く最も簡単なコードのことを「Hello World」と言いますが、ハードウェアの世界ではLEDを点滅させる「**Lチカ**」がそれに相当します。

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

#### 2-4-1. 初期化処理コードの設定  
以下のソースコードをコピーします
```javascript
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 });
```

先ほど読み込んだ`obniz repeat`をダブルクリックで選択し、プロパティの鉛筆マークを選択

<a href="https://gyazo.com/70bcaceaeaba113cc79960839c18ad38"><img src="https://gyazo.com/70bcaceaeaba113cc79960839c18ad38.png" alt="Image from Gyazo" width="374"/></a> 

表示された初期化処理という記入場所にコードを貼り付けし更新を押します。

<a href="https://gyazo.com/ae374efbb8811de4f32e8262a6db4a43"><img src="https://gyazo.com/ae374efbb8811de4f32e8262a6db4a43.png" alt="Image from Gyazo" width="374"/></a> 

### 2-5. やってみよう

設定が完了したら右上のデプロイボタンをクリック

<a href="https://gyazo.com/ef06153ec135eeb14e04ce4885e9369d"><img src="https://gyazo.com/ef06153ec135eeb14e04ce4885e9369d.png" alt="Image from Gyazo" width="374"/></a>  

### 3-1. 完成イメージ

[![Image from Gyazo](https://gyazo.com/17852495dc721319ae13da119fa852d7.gif)](https://gyazo.com/17852495dc721319ae13da119fa852d7)

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



