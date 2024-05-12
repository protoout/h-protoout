# L01-生成AI: 生成AIと一緒にNode-RED開発

生成AIを使ってコードを書いてみましょう。

今回このクラスではNode-REDを使ったローコード開発をしていますが、ChatGPTを活用して開発を便利にすることができます。

## 0. Function GPTノードの紹介とやること （紹介のみ）

[Function GPT](https://github.com/FlowFuse/node-red-function-gpt)というChatGPT(GPT)を組み込んだノードがあります。

> <img src="https://i.gyazo.com/ac8b8206e2ad031d7295ead93b479228.png" width="200px">
> <img src="https://i.gyazo.com/b5c4e6d65c879e267ed03d335a382f45.gif" width="400px" />

このノードを使うと日本語で指示を出してFunctionノードで内部で使えるコード（JavaScriptというプログラミング言語）を生成してくれます。

日本語で指示を出す -> プログラムが生成される -> Node-REDで実行
（絵が欲しい）

という流れで日本語で指示を出すと翻訳してくれます。

生成されたコードが正しく動作するかどうかですが、小さな処理単位だとかなりよい精度で動いてくれます。

### 今回はこれと同様のことをChatGPTを使って進めてみます。

`Function GPTノード`はAPIキーを発行して利用するのですが、授業で全員でやるとトラブルがある可能性もあるので`Function GPTノード`は使わずに、同様のことをChatGPT(GPT3.5)を使ってやってみます。

■前提: ここではChatGPTを使うので、OpenAIのアカウントを作成[ChatGPT](https://chat.openai.com/)を開き、アカウントを作成してください。すでに持っている方はあるもので構いません。

## 1. ChatGPTでコード生成

先ほど紹介したプロンプトエンジニアリングの要領で、ChatGPTに役割を与えて精度を上げることができます。

Function GPTの内部で使われていたプロンプト（AIへの指示文章）を元にサンプルを作りました。

### 1-1. ChatGPTに聞く

[こちら](../../../tools/prompt-sample.md)のプロンプトをコピーしてChatGPTに投げてみましょう。

今回は"距離センサーの値が300以下かどうかで処理を変えてみる"処理を試してみます。

> <img src="https://i.gyazo.com/43947e8bdf8966239e6c518202bb1836.png" width="400px">

### 1-2. functionノードに生成されたコードを貼る

生成されたコードを貼り付けましょう。

> <img src="https://i.gyazo.com/34db1703d27e38783e5edd9913a8d88b.gif" width="400px" />

### 1-3. injetcとchangeノードでセンサーのエミュレート処理

本当は`onbiz repeatノード`で試すのが良いですが、接続トラブルがあるとよくないので代わりに`injectノード`と`chageノード`を使ってセンサーデータが送られてきた様子をエミュレート（再現・模倣）します。

> <img src="https://i.gyazo.com/08f2c93b8b66e11a0c46261de52bd8b4.png" width="400px" />

`chagenノード`は仮のセンター値として200を設定してみましょう。最後にデバッグノードも接続してください。

> <img src="https://i.gyazo.com/9f49b4e236e858d42b3b24dc57f47db9.gif" width="400px" />

<details><summary>（本当はこんな感じで距離センサーを繋げたいです。進行が早い人はこちらをやってみてください。）クリックで開く</summary>

[超音波距離センサーのマニュアル](../../../tools/parts-manual/sensor/distance.md)を見つつ、`設定ノード`と`obniz repeatノード`を設定しましょう。

> obniz repeatノードの中身の例
> <img src="https://i.gyazo.com/5c9b728c9189d1d6ef96c29edd30f6a3.png" width="400px" />

> <img src="https://i.gyazo.com/a580726d604b624446a4c2eebd30d6c8.png" width="400px" />

</details>

### 1-4. 試してみる

`injectノード`の左のボタンを押して発火してみましょう。200というセンサーデータが`functionノード`に送られ、内部では **ChatGPTが書いてくれたコードが処理をしてセンサーデータが300以下なのかどうかを判定**してくれています。

<img src="https://i.gyazo.com/b319f1c135968a407ac1f1dae8238e23.png" width="400px" />

画像のようにデバッグノードに200というデータが出れば成功です。
`chagneノード`の値を400などに変更して再度試すとおそらく反応がないと思います。これは300以下のときのみ反応させたかったので正常な挙動です。

**[◀ 目次ページに戻る](../readme.md)**