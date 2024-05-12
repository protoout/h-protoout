# L01-生成AI: 生成AIと一緒にNode-RED開発

生成AIを使ってコードを書いてみましょう。

今回このクラスではNode-REDを使ったローコード開発をしています。

Node-REDにインポートできる形式で、Node-REDのフローをかいてもらうという使い方ができます。

## 紹介のみ - Function GPTノード

[Function GPT](https://github.com/FlowFuse/node-red-function-gpt)というChatGPT(GPT)を組み込んだノードがあります。
> <img src="https://i.gyazo.com/ac8b8206e2ad031d7295ead93b479228.png" width="200px">
> <img src="https://i.gyazo.com/b5c4e6d65c879e267ed03d335a382f45.gif" width="450px" />

このノードを使うと日本語で指示を出してFunctionノードで内部で使えるコード（JavaScriptというプログラミング言語）を生成してくれます。

日本語で指示を出す -> プログラムが生成される -> Node-REDで実行
（絵が欲しい）

という流れで日本語で指示を出すと翻訳してくれます。

生成されたコードが正しく動作するかどうかですが、小さな処理単位だとかなりよい精度で動いてくれます。

### 今回はこれと同様のことをChatGPTを使って進めてみます。

Function GPTノードはAPIキーを発行して利用するのですが、授業で全員でやるとトラブルがある可能性もあるので同様のことを

## 0. 前提

ここではChatGPTを使うので、OpenAIのアカウントを作成[ChatGPT](https://chat.openai.com/)を開き、アカウントを作成してください。すでに持っている方はあるもので構いません。

## 1. 

2. プロンプトを書き、ChatGPT/Gemini/Claudeのいずれかにフローを生成してもらう

```

以下のように動作するNode-REDのフローJSONを出力してください

- 3つのInjectノードではじまる。それぞれのノードは、payloadにりんご・みかん・バナナと入力。
- 3つのinjectノードからswitchノードにつなぎ、switchノードからchangeノードにつないで
    - りんごの場合: 赤を出力
    - みかんの場合: オレンジを出力
    - バナナの場合: 黄色を出力
- debugノードにレスポンスを表示する

```

3. 出力をインポートする
Node-REDのインポート機能で、出力されたJSONデータを貼り付けし、インポートしてください。


右上のメニューから「読み込み」を選択。

<img src="https://i.gyazo.com/04f8550740b64f749070f06fbf08dcfa.jpg" width="500px" alt="Image 3">


生成AIの出力結果をコピー

<img src="https://i.gyazo.com/0ff565919c19f27583766f0337e4754f.png" width="500px" alt="Image 3">


先ほどコピーしたものを貼り付け

<img src="https://i.gyazo.com/212c2329c8a8a09ea1633130d94bdb82.png" width="500px">


ちょうどよい場所でクリック

<img src="https://i.gyazo.com/b1a791c700d1dd982192dd826fa7854b.gif" width="500px">


デプロイして、指定した通り動くか試してみましょう！

<img src="https://i.gyazo.com/899837fd64bfcfb1b23cd574edbf4775.png" width="500px" alt="Image 3">


## もう少し、ふんわりとしたプロンプトを試してみる

さきほどの事例では、どのノードを使うかまでプロンプト内で指定していました。

今度は、もうすこし抽象的なプロンプトで試してみましょう。


```
以下のように動作するNode-REDのフローJSONを出力してください

obnizノードを使ってサーボモーターを動かす。
60度になったら120度に変える
120度になったら60度に変える
これを1秒ごとに繰り返す

```




---

**[◀ 目次ページに戻る](./readme.md)**