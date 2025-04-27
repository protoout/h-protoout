# 好きな曲を流すには...  
  
先ほどの演習では、ドレミをどのように鳴らすかを知ることができました。  
  
### ■[**obniz x Node-REDマニュアル: アクチュエーター: スピーカー（ブザー）**](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-speaker)

```js
//ドの音
obnizParts.speaker.play(523);
await obniz.wait(500); // 0.5秒待つ

// レの音
obnizParts.speaker.play(587);
await obniz.wait(500); // 0.5秒待つ

// ミの音
obnizParts.speaker.play(659);
await obniz.wait(500); // 0.5秒待つ

```

これを使えば曲を奏でることも可能ですね。  
では、生成 AI を使って、曲のサンプルコードをつくってもらいましょう。  

どんな指示を出したら Node-RED で動くのか、考えながらやってみましょう！！

### プロンプト例
<details>

<summary>コーディングの依頼例</summary>

```
ブザー(PKM13EPYH4000-A0)を使って曲を奏でたいです。
次のJavaScriptのコードをもとにして【曲名】のメロディーを書いてください。

obnizParts.speaker.play(523); // ドの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.play(587); // レの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.play(659); // ミの音を鳴らす
await obniz.wait(1000); //1秒待つ
obnizParts.speaker.stop();

```

</details>  


### コード例
<details>

<summary>「うっせぇわ」</summary>

```js
async function playUsseewaIntro() {
    const notes = [
        784, 784, 880, 784, 659, 784, 659, 587
    ];
    const durations = [
        300, 300, 300, 300, 300, 300, 300, 500
    ];

    for (let i = 0; i < notes.length; i++) {
        obnizParts.speaker.play(notes[i]);
        await obniz.wait(durations[i]);
        obnizParts.speaker.stop();
        await obniz.wait(100);
    }
}

playUsseewaIntro();

```

</details>  

<details>  
<summary>「きらきら星」</summary>

```js
async function playTwinkle() {
    const notes = [
        523, 523, 784, 784, 880, 880, 784, // きらきらひかる
        698, 698, 659, 659, 587, 587, 523  // おそらのほしよ
    ];
    const durations = [
        500, 500, 500, 500, 500, 500, 1000,
        500, 500, 500, 500, 500, 500, 1000
    ];

    for (let i = 0; i < notes.length; i++) {
        obnizParts.speaker.play(notes[i]);
        await obniz.wait(durations[i]);
        obnizParts.speaker.stop();
        await obniz.wait(100); // 少し休符を入れる
    }
}

playTwinkle();

```

</details>  

----

**[◀ Lesson1に戻る](./readme.md)**
