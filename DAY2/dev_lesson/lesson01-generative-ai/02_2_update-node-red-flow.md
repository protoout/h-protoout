# L01-生成AI: ChatGPTと一緒にNode-REDでIoT開発 2/3

まだイメージが掴めてないと思いますが、引き続きやっていきましょう。

距離センサーとスピーカーを連携させる仕組みが出来上がっていくまで少し辛抱してくださいませ。

## 2. ChatGPTに聞いて条件分岐をしてみる

先ほどのプロンプトを変更して、以下のような状態を作ってみます。

> 一旦、目指す形
> 
> <img src="https://i.gyazo.com/b0cd6ddabeb3e90fc7c261a8c04f702e.png" width="400px" />

注目すべきは`Functionノード`から出力が二つに増えている箇所です。

### 2-1. ChatGPTに再度聞いてみます。

[サンプル](../../../tools/prompt-sample.md)を参考に、以下のようなプロンプトをChatGPTに聞いてみましょう。

`# system`の箇所は先ほど同様で`# prompt`の部分を変更しています。

```
## system
- 常にNode-REDのFunctionノードで利用できるコンテンツを返してください。
- 常にvarの代わりにconstかletを使います。
- 外部のノードモジュールを使用するように要求されない限り、require() を使用しないでください。
- 指示がない限り、基本的にコードとインラインコードコメントを返します。

## prompt
センサーの値が送られてきます。センサーデータを元にセンサーの値が300以下かどうかで条件分岐して次のノードに渡す処理を書いて下さい。条件分岐をして二つの出力先が作れるようにしてください。
```

"二つの出力先が作れるようにしてください。"などの **日本語でやりたいことを具体的に伝えるような文章**を書いています。

これは **日本語の指示の出し方で精度が変わる**ので、僕よりも皆さんの方が良い文章を書いてAIと仲良くなれるかもしれません。

さて、コードが新たに出力されるのでそのコードを`Functionノード`に上書きします。

<details><summary>（おそらくこんなコードが出力されます）クリックで開く</summary>

```js
const sensorValue = msg.payload;

if (sensorValue <= 300) {
    // センサーの値が300以下の場合の処理
    return [msg, null]; // 一つ目の出力先にメッセージを渡し、二つ目の出力先はnull
} else {
    // センサーの値が300より大きい場合の処理
    return [null, msg]; // 一つ目の出力先はnull、二つ目の出力先にメッセージを渡す
}
```

</details>

### 2-2. Functinノードの編集

生成されたコードを`Functionノード`に上書きします。

> <img src="https://i.gyazo.com/dae27d7e4fd699cc4d277efac533f5ed.gif" width="400px" />

次に、 **設定タブから出力数を2に変更**しましょう。これで出力先を増やすことができます。 ついでに **名前も分かりやすく変更**しておきましょう。

> <img src="https://i.gyazo.com/d422299fd554104f0af903c69cd06f79.png" width="400px" />

### 2-3. templateノードの設定

次に`templateノード`を設定します。2つの条件分岐にそれぞれ設定してください。

> <img src="https://i.gyazo.com/2b59972cc69fecf876e08ae837a47d2f.png" width="400px" />

`templateノード`の上側に設置した方には`近い`などの文言を入れてみましょう。

> 例: `300以下！近い！: {{payload}} !`
> <img src="https://i.gyazo.com/5ea08b5cf73fa128bbc620d040eee29b.gif" width="400px" />

下側のもう一つの`templateノード`は逆に`遠い`などの文言を入れてみましょう。

> <img src="https://i.gyazo.com/62d9865932a1231c058a13de048e51b1.png" width="400px" />

### 2-4. 試してみる

`chagenノード`の値を変えて`injectノード`を発火させると条件によって違った文言が右側のデバッグコンソールに表示されます。

> <img src="https://i.gyazo.com/56da9a10d216f2c659c952f9489b6350.png" width="400px" />

うまく条件分岐ができていますね。

### 2-5. 少しコードを見てみる

ChatGPTに聞くことで、おそらくこんなコードが生成されていると思います。

```js
// センサーデータを受け取る
const sensorValue = msg.payload;

// センサーの値が300以下かどうかをチェックする
if (sensorValue <= 300) {
    // センサーの値が300以下の場合の処理
    return [msg, null];
} else {
    // センサーの値が300より大きい場合の処理
    return [null, msg];
}
```

細かくは説明しませんが、「`if (sensorValue <= 300)`という箇所でセンサーの値の条件を判定して、`return [msg, null];`や`return [null, msg];`の箇所で次の出力先にデータを送っていそう......かも」くらいがイメージつくと嬉しいです。

これくらいのイメージがあると制作をやっていくときに少し楽になります。

### 2-6. (セーブポイント)

ここまでの手順で詰まってしまった人はこちらのここまでの完成版フローを読み込んでみましょう。

```json
[{"id":"949bcb5b767d631e","type":"function","z":"dcb0e5384efb4848","name":"300で条件分岐","func":"// センサーデータを受け取る\nconst sensorValue = msg.payload;\n\n// センサーの値が300以下かどうかをチェックする\nif (sensorValue <= 300) {\n    // センサーの値が300以下の場合の処理\n    return [msg, null];\n} else {\n    // センサーの値が300より大きい場合の処理\n    return [null, msg];\n}","outputs":2,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":380,"y":140,"wires":[["6c9a26c5a057232e"],["ab70f60582030ae5"]]},{"id":"fb5e5fa71ac43ccd","type":"inject","z":"dcb0e5384efb4848","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":140,"y":60,"wires":[["f654e83f62a59fa0"]]},{"id":"f654e83f62a59fa0","type":"change","z":"dcb0e5384efb4848","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"200","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":260,"y":100,"wires":[["949bcb5b767d631e"]]},{"id":"58e4d6e5a85497f0","type":"debug","z":"dcb0e5384efb4848","name":"debug 12","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":700,"y":180,"wires":[]},{"id":"6c9a26c5a057232e","type":"template","z":"dcb0e5384efb4848","name":"近い","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"300以下！近い！: {{payload}} !","output":"str","x":530,"y":140,"wires":[["58e4d6e5a85497f0"]]},{"id":"ab70f60582030ae5","type":"template","z":"dcb0e5384efb4848","name":"遠い","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"300より大きい {{payload}} 遠い!","output":"str","x":530,"y":180,"wires":[["58e4d6e5a85497f0"]]}]
```

**[◀ 目次ページに戻る](../readme.md)**