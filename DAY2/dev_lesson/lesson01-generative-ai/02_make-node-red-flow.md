# L01-生成AI: 生成AIと一緒にNode-RED開発

生成AIを使ってコードを書いてみましょう。

今回このクラスではNode-REDを使ったローコード開発をしていますが、ChatGPTを活用して開発を便利にすることができます。

## 0. Function GPTノードの紹介とやること （紹介のみ）

[Function GPT](https://github.com/FlowFuse/node-red-function-gpt)というChatGPT(GPT)を組み込んだノードがあります。

> <img src="https://i.gyazo.com/ac8b8206e2ad031d7295ead93b479228.png" width="200px">
> <img src="https://i.gyazo.com/b5c4e6d65c879e267ed03d335a382f45.gif" width="450px" />

このノードを使うと日本語で指示を出してFunctionノードで内部で使えるコード（JavaScriptというプログラミング言語）を生成してくれます。

日本語で指示を出す -> プログラムが生成される -> Node-REDで実行
（絵が欲しい）

という流れで日本語で指示を出すと翻訳してくれます。

生成されたコードが正しく動作するかどうかですが、小さな処理単位だとかなりよい精度で動いてくれます。

### 今回はこれと同様のことをChatGPTを使って進めてみます。

`Function GPTノード`はAPIキーを発行して利用するのですが、授業で全員でやるとトラブルがある可能性もあるので`Function GPTノード`は使わずに、同様のことをChatGPT(GPT3.5)を使ってやってみます。

### 前提

ここではChatGPTを使うので、OpenAIのアカウントを作成[ChatGPT](https://chat.openai.com/)を開き、アカウントを作成してください。すでに持っている方はあるもので構いません。

## 1. ChatGPTでコード生成

先ほど紹介したプロンプトエンジニアリングの要領で、ChatGPTに役割を与えて精度を上げることができます。

Function GPTの内部で使われていたプロンプト（AIへの指示文章）を元にサンプルを作りました。

- ChatGPTに聞く

[こちら](../../../tools/prompt-sample.md)のプロンプトをコピーしてChatGPTに投げてみましょう。

<img src="https://i.gyazo.com/43947e8bdf8966239e6c518202bb1836.png" width="400px">

- functionノードに生成されたコードを貼る

<img src="https://i.gyazo.com/34db1703d27e38783e5edd9913a8d88b.gif" width="400px" />


**[◀ 目次ページに戻る](../readme.md)**