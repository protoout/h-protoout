# スピーカーで音を鳴らしてみよう


### **新しいことをはじめる前に※**  

[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。

---

## 1.やってみよう

<a href="https://gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57"><img src="https://i.gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57.jpg" alt="Image from Gyazo" width="700"/></a>

任意の高さの音を出すことができるスピーカーです。  
「インジケーター」の1つで、これ1つでブザーやアラームといった通知系デバイスを作ることができます。

保護紙をつまんでまっすぐスピーカーを引っ張ると抜き取ることができます。  

### 1-1. obnizとの接続

<a href="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf"><img src="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf.jpg" alt="Image from Gyazo" width="700"/></a>

obnizの0番と1番の端子に差し込みます。  
極性（方向）はなく、どちらの向きで差し込んでも大丈夫です。

### 1-2. obnizの公式ページから動作を確認する

次は先に、obnizの公式ドキュメントからサンプルを実行してみましょう。  
温度センサーのときを思い出しながら、以下のリンクにアクセスして音を鳴らしてみてください。  
サンプルは `play(frequency)` と書かれている場所のものを使いましょう。

[Speaker | JS Parts Library | obniz](https://docs.obniz.com/ja/sdk/parts/Speaker/README.md)

![image.png (51.5 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/3641c01c-67aa-4150-8074-b4c949fd16c7.png)

サンプルは、ブラウザ上で直接コードを書き換えることができます。  
1000Hzと書いてある部分を、500や1500など好きな値に変更して再実行し、音が変化していることを確認してください。  
参考：[音階周波数](https://tomari.org/main/java/oto.html)

> 音楽好きであれば、これ1つで楽器を作るのも楽しいかもしれません！

### 1-3. Node-REDで実行

以下のフローを読み込み、Node-REDで動かしてみましょう。


```json
[{"id":"9684e82d.a3b478","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nif (msg.payload === 'push') {\n    // 押されたとき\n    obniz.display.clear(); // 画面を消去\n    obniz.display.print('beep!');  // beep! と画面に表示\n    obnizParts.Speaker.play(1000); // 1000Hz で音を鳴らす\n} else {\n    // 何も押していない\n    obniz.display.clear(); // 画面を消去\n    obniz.display.print('silent');  // silent と画面に表示\n    obnizParts.Speaker.stop(); // 音をとめる\n}\n\nreturn msg;","x":270,"y":280,"wires":[["f8e3da0b.78b968"]]},{"id":"f8e3da0b.78b968","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":470,"y":280,"wires":[]}]
```
▼読み込み結果  
<a href="https://gyazo.com/c5e4d78c48e149bd3c50c56423a76289"><img src="https://gyazo.com/c5e4d78c48e149bd3c50c56423a76289.png" alt="Image from Gyazo" width="374"/></a>  


Lチカ同様、読み込んだ`obniz repeat`をダブルクリックで選択し、プロパティの鉛筆マークから、初期化処理フローを**上書き更新**してください。
（Lチカの時に張り付けたコードは消してください）

▼初期化処理フロー
```json
obnizParts.Speaker = obniz.wired("Speaker",{ signal:0, gnd:1 });
```

スイッチを押したり離したりして、スピーカーのコントロールができます。


## 2.演習

### 2-1. 好きな音を出そう

ブザーから任意の音程を出してみましょう

| 音階 | 周波数[Hz] |
| ---- | ---------- |
| ド   | 523        |
| レ   | 587        |
| ミ   | 659        |
| ファ | 698        |
| ソ   | 784        |
| ラ   | 880        |
| シ   | 988        |
| ド   | 1046       |


### 2-2.【応用】 楽器をつくってみよう

ブザーから色々な音を出せる楽器を考えて作ってみましょう。


サンプルコード: obnizのスイッチを右に倒すと半音ずつ音が上がり、左に倒すと半音ずつさがります。
```json
[{"id":"d8389f17.33ec7","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nlet freq = context.get('freq')||523; // 周波数用のコンテキストを参照（無ければ初期化）\nlet note_number = context.get('note')||72; // MIDIノート番号// ノート番号用のコンテキストを参照（無ければ初期化）\n\nobniz.display.clear(); // 画面を消去\n\nif (msg.payload === 'push') {\n // スイッチが押されている状態\n obnizParts.Speaker.play(freq); // 音を鳴らす\n} else if (msg.payload === 'right') {\n // 右にスイッチを倒したとき\n if (note_number < 127) note_number++; // ノート番号+1\n freq = Math.round(440 * (2 ** ((note_number - 69) / 12))); // 周波数を再計算\n} else if (msg.payload === 'left') {\n // 左にスイッチを倒したとき\n if (note_number > 0) note_number--; // ノート番号-1\n freq = Math.round(440 * (2 ** ((note_number - 69) / 12))); // 周波数を再計算\n} else {\n // スイッチが押されていない状態\n obnizParts.Speaker.stop(); // 音を停止する\n}\ncontext.set('freq',freq);//現在の周波数をコンテキストへ保存\ncontext.set('note',note_number);//現在のノート番号をコンテキストへ保存\nobniz.display.print(freq); // 現在の周波数を表示\n\nreturn msg;","x":270,"y":280,"wires":[["4855899b.7e8ee8"]]},{"id":"4855899b.7e8ee8","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":450,"y":280,"wires":[]}]
```


---

**[◀ 目次ページに戻る](../readme.md)**