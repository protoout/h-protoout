# L01-2. 生成AIコーディング: ChatGPTと一緒にNode-REDでIoT開発 1/3

生成AIの活用ポイントはたくさんありますが、取り急ぎ今回はChatGPTを使ってプロトタイピングに役立たせてみましょう。

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

### この章を進めると出来るもの

ここで作るものは超音波距離センサーとスピーカーの連携で、`手をかざすと音が鳴って、手を遠ざけると音が止まる`仕組みを作ってみます。

> 完成イメージ（動画です。右クリックから別タブで開いてみましょう。）
> 
> [<img src="https://i.gyazo.com/b8d54909da2960018e032e9b4df4e863.png" width="400px" />](https://twitter.com/n0bisuke/status/1789748155984052702)

## 1. ChatGPTでコード生成

[プロンプトエンジニアリング](https://aws.amazon.com/jp/what-is/prompt-engineering/#:~:text=%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E3%83%AA%E3%83%B3%E3%82%B0%E3%81%A8%E3%81%AF%E3%80%81%E7%94%9F%E6%88%90,%E3%81%AA%E6%8C%87%E7%A4%BA%E3%81%8C%E5%BF%85%E8%A6%81%E3%81%A7%E3%81%99%E3%80%82)と呼ばれる、より適切に生成AIに命令を出し、良い結果を引き出す手法があります。

細かくは色々ありますが、AIに役割を与えて精度を上げることができます。

今回、`Function GPTノード`の内部で使われていたプロンプト（AIへの指示文章）を元にサンプルを作りました。

### 1-1. 演習: ChatGPTに聞く

こちらのプロンプトサンプルから[１. Node-REDのFunctionノードで使えるコードを生成](../../../tools/prompt-sample.md)のプロンプトをコピーしてChatGPTに投げてみましょう。

今回は"距離センサーの値が300以下かどうかで処理を変えてみる"処理を試してみます。

> <img src="https://i.gyazo.com/43947e8bdf8966239e6c518202bb1836.png" width="400px">

プログラムが生成されます。あっと言う間ですね。

**人間はプログラムを書かずに日本語で指示出しをしてAIがプログラムを代わりに書いてくれるという体験**です。👏👏👏👏

一度どんな日本語でChatGPTに指示を出しているか、も少し確認してみましょう。

### 1-2. Functionノードに生成されたコードを貼る

生成されたコードを`Functionノード`に貼り付けましょう。

> <img src="https://i.gyazo.com/34db1703d27e38783e5edd9913a8d88b.gif" width="400px" />

### 1-3. InjetcとChangeノードでセンサーのエミュレート処理

本当は`onbiz repeatノード`で試すのが良いですが、接続トラブルがあるとよくないので、まずは代わりに`Injectノード`と`Chageノード`を使ってセンサーデータが送られてきた様子をエミュレート（再現・模倣）します。

> <img src="https://i.gyazo.com/08f2c93b8b66e11a0c46261de52bd8b4.png" width="400px" />

`Changeノード`は仮のセンター値として200を設定してみましょう。最後にデバッグノードも接続してください。

> <img src="https://i.gyazo.com/9f49b4e236e858d42b3b24dc57f47db9.gif" width="400px" />

<details><summary>（本当はこんな感じで距離センサーを繋げたいです。進行が早い人はこちらをやってみてください。）クリックで開く</summary>

[超音波距離センサーのマニュアル](../../../tools/parts-manual/sensor/distance.md)を見つつ、`設定ノード`と`obniz repeatノード`を設定しましょう。

> `obniz repeatノード`の中身の例
> <img src="https://i.gyazo.com/5c9b728c9189d1d6ef96c29edd30f6a3.png" width="400px" />

> <img src="https://i.gyazo.com/a580726d604b624446a4c2eebd30d6c8.png" width="400px" />

</details>

### 1-4. 試してみる

`Injectノード`の左のボタンを押して発火してみましょう。200というセンサーデータが`Functionノード`に送られ、内部では **ChatGPTが書いてくれたコードが処理をしてセンサーデータが300以下なのかどうかを判定**してくれています。

> <img src="https://i.gyazo.com/b319f1c135968a407ac1f1dae8238e23.png" width="400px" />

画像のようにデバッグノードに200というデータが出れば成功です。

`Chagneノード`の値を400などに変更して再度試すとおそらく反応がないと思います。これは300以下のときのみ反応させたかったので正常な挙動です。

ちょっとまだイメージしにくいかもしれませんが、自身でプログラムを書かずに生成AIにプログラムを書かせての開発がやれてしまっています。👏👏👏

### 1-5. （セーブポイント）

ここまでの手順で詰まってしまった人はこちらのここまでの完成版フローを読み込んでみましょう。

```json
[{"id":"ad667d104f251cf4","type":"function","z":"dcb0e5384efb4848","name":"function 1","func":"// センサーデータを受け取る\nconst sensorValue = msg.payload;\n\n// センサーの値が300以下かどうかをチェックする\nif (sensorValue <= 300) {\n    // センサーの値が300以下の場合の処理\n    return msg;\n} else {\n    // センサーの値が300より大きい場合は何もしない\n    return null;\n}","outputs":1,"timeout":0,"noerr":0,"initialize":"","finalize":"","libs":[],"x":320,"y":140,"wires":[["857861444cbcd775"]]},{"id":"ae2e5ee5b4fda98c","type":"inject","z":"dcb0e5384efb4848","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":100,"y":40,"wires":[["e6198ac87332ac9e"]]},{"id":"e6198ac87332ac9e","type":"change","z":"dcb0e5384efb4848","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"400","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":220,"y":100,"wires":[["ad667d104f251cf4"]]},{"id":"857861444cbcd775","type":"debug","z":"dcb0e5384efb4848","name":"debug 10","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":420,"y":180,"wires":[]}]
```

**[◀ 目次ページに戻る](../readme.md)**