# Lチカしてみよう


<img src="https://i.gyazo.com/23a5a24bdd5a812ed8baf83ced57b590.jpg" alt="Image from Gyazo" width="500"/>

ソフトウェアの世界では一番最初に書く最も簡単なコードのことを「Hello World」と言いますが、ハードウェアの世界ではLEDを点滅させる「**Lチカ**」がそれに相当します。

<details>
<summary>(補足)LEDと抵抗の切っても切れない関係</summary>

<img src="https://i.gyazo.com/4affed7a9a893c86880d9ff974562cf4.jpg" alt="Image from Gyazo" width="500"/>

<img src="https://i.gyazo.com/1e31004da05e837a9c631917b606c27e.png" alt="Image from Gyazo" width="500"/>
本来、LEDは必ず抵抗とセットで使うのが電子工作における決まりごとになっていますが、今回は抵抗が内蔵されたLEDを利用するため、これ1つを直接obnizに接続することで制御ができます。
</details>

### 1-1. まずは光らせてみよう

<img src="https://i.gyazo.com/4bb4d4af379c881b0f68274869c18505.png" alt="Image from Gyazo" width="500"/>

脚の長いほうがアノード、短いほうをカソードといいます。  

obnizに電源が入っている状態で、写真のように  

- LEDの長い脚（アノード）をobnizの＋端子
- LEDの短い脚（カソード）をobnizの－端子

に接続してみてください。光りましたか？

> - 光らない場合は、以下を確認しましょう。
>   - 脚が逆になっていないか
>   - 3つある穴の中央に挿していないか（両脇の穴を使ってください）

obnizのプラス端子とマイナス端子を繋ぐことで通電し、LEDが光るようになります。

### 1-2. obnizで制御できるように接続

<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" alt="Image from Gyazo" width="500"/>

- LEDの長い脚をobnizの0番
- LEDの短い脚をobnizの1番

に接続してください。

### 1-3. obnizの公式ページから動作を確認する

obniz公式のドキュメントには「Parts Library」といって、ブラウザから簡単にパーツを試せるツールが用意されています。 
まずはNode-REDではなく、obnizの「Parts Library」からLEDを試してみましょう。

[LED | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

このドキュメントページの中の `on` と書かれているサンプルを探し、自分のobniz IDを入力して `実行` をクリックしてみましょう。

[![Image from Gyazo](https://i.gyazo.com/eeec7fc6bb18ee0ff4767e8d6d1d2946.png)](https://gyazo.com/eeec7fc6bb18ee0ff4767e8d6d1d2946)


確認が終わったら必ず閉じてobnizの処理を止めるようにしてください。

停止しないと他のコードを実行できません。

obnizのディスプレイにQRコードとobniz IDが表示されていれば、処理は停止できています。

<a href="https://gyazo.com/f4015ac1a321312a399818c810063ee5"><img src="https://i.gyazo.com/f4015ac1a321312a399818c810063ee5.png" alt="Image from Gyazo" width="500"/></a>

`off`や`blink`なども実行してみましょう！


#### 1-3-1. 「Parts Library」から実行できるのはLEDだけじゃないです

「[obniz Parts Library](https://docs.obniz.com/ja/sdk/parts)」に掲載されている電子部品であれば、どれでも簡単に動作確認をすることができます。

1. ドキュメントの指示通りに接続  
2. 自分のobniz IDを入力  
3. `実行`をクリック  
のわずか3ステップで動作確認を行うことができます。便利！

新しい電子部品を自分で使ってみるときは、まずこの「obniz Parts Library」に使いたい電子部品と同じか、似たようなものがないかを調べ、できるだけ対応した（掲載されている）部品を使うようにするとすぐに動作確認ができるのでオススメです。


### 1-4. Node-REDで実行

<a href="https://gyazo.com/17852495dc721319ae13da119fa852d7"><img src="https://i.gyazo.com/17852495dc721319ae13da119fa852d7.gif" alt="Image from Gyazo" width="500"/></a>

以下のフローを読み込み、初期化ノードを設定することで、Node-REDで動かしてみましょう。  
  

#### 2-4-1. フローの読み込み
まず以下のフローをNode-REDで読み込みます。

```json
[{"id":"5fa9057f.f2e0ac","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nreturn msg;","x":330,"y":340,"wires":[["ebafa559.00b978","e8f7976.0477568"]]},{"id":"ebafa559.00b978","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"obniz.display.clear(); // 画面を消去\r\n\r\nif (msg.payload === 'push') {\r\n // スイッチが押されている状態\r\n obniz.display.print('LED ON');\r\n obnizParts.led.on();\r\n} else {\r\n // スイッチが押されていない状態\r\n obniz.display.print('LED OFF');\r\n obnizParts.led.off();\r\n}\r\n","x":520,"y":340,"wires":[[]]},{"id":"e8f7976.0477568","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":510,"y":420,"wires":[]}]
```
■読み込み結果  
<a href="https://gyazo.com/cccec7050a56c2e266600819460d4694"><img src="https://i.gyazo.com/cccec7050a56c2e266600819460d4694.png" alt="Image from Gyazo" width="374"/></a>  



#### 1-4-2. 初期化処理コードの設定  
1. 以下のコードをコピーします

```javascript
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 });
```

2. 先ほど読み込んだ`obniz repeat`をダブルクリックで選択し、プロパティの鉛筆マークを選択

<a href="https://gyazo.com/70bcaceaeaba113cc79960839c18ad38"><img src="https://gyazo.com/70bcaceaeaba113cc79960839c18ad38.png" alt="Image from Gyazo" width="374"/></a> 

3. 表示された初期化処理という記入場所にコードを貼り付けし更新を押します。

<a href="https://gyazo.com/ae374efbb8811de4f32e8262a6db4a43"><img src="https://gyazo.com/ae374efbb8811de4f32e8262a6db4a43.png" alt="Image from Gyazo" width="374"/></a> 

### 1-5. 動作をためそう

設定が完了したら右上のデプロイボタンをクリック。

obnizのスイッチを押すとLEDが点灯するのを確認してください。  

<a href="https://gyazo.com/ef06153ec135eeb14e04ce4885e9369d"><img src="https://gyazo.com/ef06153ec135eeb14e04ce4885e9369d.png" alt="Image from Gyazo" width="374"/></a>  


obnizの接続がうまくいくと、アイコンが緑色になります。

赤の場合はなんらかの原因により接続できていません。

その場合は以下を試してください
- obniz IDが正しいかチェック
- obnizの電源は入っているかチェック
- Node-REDのデプロイを再度行ってみる
- 他のフローが動いている→ 停止フローをクリックして停止してから試す

<a href="https://gyazo.com/109e14de01eeb38e4bf46f7fd37337c1"><img src="https://i.gyazo.com/109e14de01eeb38e4bf46f7fd37337c1.png" alt="Image from Gyazo" width="500"/></a>


その後、obnizのボタンを操作してLEDが点灯するか試してみてください。


###  完成イメージ


<img src="https://gyazo.com/17852495dc721319ae13da119fa852d7.gif" alt="Image from Gyazo" width="500"/>

※ この画像はobniz Board（みなさんの手元にあるobniz 1Yとは異なるもの）です。



## 2.演習

### 2-1. obniz functionの中身を書き換えて、pushではなく`right`でLEDがつくように変えてみよう

obnizのスイッチは、押し込むだけでなく左右にカチカチ押すことができ、push, right, leftの3つの状態を取得することが可能です。

obniz functionの中身を書き換えて、右側に倒したときにLEDが光るように書き換えてみましょう。




### 2-2.【応用】 obnizのParts Libraryを参考に、blink();を使って指定時間後にLEDが消えるように変えてみよう

「[obniz Parts Library](https://docs.obniz.com/ja/sdk/parts/LED/README.md)」の情報を見て、

blink();を使って指定時間後にLEDが消えるように書き換えてみましょう。



---

**[◀ 目次ページに戻る](../readme.md)**