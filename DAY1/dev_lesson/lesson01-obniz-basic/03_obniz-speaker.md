# スピーカーで音を鳴らしてみよう

---

## スピーカーをつけてみよう

<a href="https://gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57"><img src="https://i.gyazo.com/c39a8d243cc56f5e5e788bcc05a68d57.jpg" alt="Image from Gyazo" width="450"/></a>

任意の高さの音を出すことができるスピーカーです。  
「インジケーター」の1つで、これ1つでブザーやアラームといった通知系デバイスを作ることができます。

保護紙をつまんでまっすぐスピーカーを引っ張ると抜き取ることができます。  

### 1. obniz Board での配線

<a href="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf"><img src="https://i.gyazo.com/76644dcdab7a2bc2b5b7a0149a2667cf.jpg" alt="Image from Gyazo" width="450"/></a>

| 電子パーツの脚         | 接続先         |
|--------------|---------------|
| スピーカーの脚 |   0   |
| スピーカーの脚  |   1   |

obnizの0番と1番の端子に差し込みます。(LED は obniz Board のディスプレイが QRコードの画面になっていたら抜いてしまって大丈夫です )  
極性（方向）はなく、どちらの向きで差し込んでも大丈夫です。



### 2. 使うノードとつなぎ方

以下のフローを読み込み、Node-REDで動かしてみましょう。

- `injectノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`
  
<img width="450" alt="image" src="https://github.com/user-attachments/assets/13e0292e-ed13-4964-ae09-29432815ad0e" />

### 3. 初期化処理コードの編集

LED 同様、 `obniz-repeatノード`をダブルクリックで選択し、プロパティのペンマークから、初期化処理コードを**書き替えて更新**してください。
（Lチカの時に張り付けたコードは消してください）

```javascript
obnizParts.Speaker = obniz.wired("Speaker",{ signal:0, gnd:1 });
```

### 4. 各ノードの設定方法

- `changeノード`

msg.payloadを「数値」「500」（数字は任意で変更してください。単位はヘルツ。）

  
<img width="450" alt="image" src="https://github.com/user-attachments/assets/2b9aa3c7-215f-4785-b8b8-b77737c900b3" />

- `obniz-functionノード`

```js
obnizParts.speaker.play(msg.payload); // msg.payloadで受け取った値（ヘルツ）の音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.stop(); //止める
```

## 5. 結果

1000Hzの音が鳴り、1秒すると止まる。

> [!CAUTION]
> **`obniz-close` で停止するのをお忘れなく！**  

## 参考：

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

---

**[◀ 目次ページに戻る](../readme.md)**
