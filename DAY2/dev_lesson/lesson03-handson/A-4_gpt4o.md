# A-4. ハンズオン: 世界最速！GPT-4oを組み込んだアプリを自分で作ってみよう

GPT-4oを組み込んだアプリを自分で作ってみましょう。

解説を入れながら紹介してきます。

## 1. ハンズオンで作るもの

冒頭に紹介したOCRの例を作る方法を紹介します。

このハンズオンではOCR機能を作りつつ、プロンプトを入れ替えることで別のアプリケーションにすることもできます。

> <img src="https://i.gyazo.com/f817c26f2a9ee46d87e949d93c7a2751.png" width="400px" />

## 2. 利用するノードの準備

## 2-1. ノードのインストール

すでにインストールしているとは思いますが、まだの方はこれらをインストールしましょう。

- `node-red-node-base64`
    - 画像をBase64という形式に変換してくれます。
    - https://flows.nodered.org/node/node-red-node-base64
- `node-red-contrib-browser-utils`
    - カメラを使えるようになります。
    - https://flows.nodered.org/node/node-red-contrib-browser-utils
- `node-red-contrib-image-output`
    - 撮影した画像のプレビューができるようになります。
    - https://flows.nodered.org/node/node-red-contrib-image-output
- `node-red-contrib-openai`
    - OpenAIのAPI（後半で説明があります。）にアクセスする機能です。
    - https://flows.nodered.org/node/node-red-contrib-openai


### 2-2. フローを作ってみる

以下のようにフローを組んでみましょう。

- `Cameraノード`
- `Image previewノード`
- `base64ノード`
- `OpenAIノード`
- `Switchノード`
- `Debugノード`

を使います。

> <img src="https://i.gyazo.com/f568c4c8177a2f9404309676d2a77e54.gif" width="400px" />


### 2-3. Functinノードの編集

Functinノードに以下のコードを上書きして貼り付けます。

```js
msg.api = 'chat/completions';
msg.params = {
    model: "gpt-4o",
    max_tokens: 1024,
    messages: [
      {
        role: "system",
        content: "You are an Optical Character Recognition (OCR) machine. You will extract all the characters from the image file in the URL provided by the user, and you will only privide the extracted text in your response. As an OCR machine, You can only respond with the extracted text."
      },
      {
        role: "user",
        content: [
          { type: "text", text: "Please extract all characters within the image. Return the only extacted characters." },
          {
            type: "image_url",
            image_url: {
              "url": `data:image/jpeg;base64,${msg.payload}`
            },
          },
        ],
      },
    ],
  }
return msg;
```

> <img src="https://i.gyazo.com/d30ee9df94d42e17d35ecf966c2a20c4.png" width="400px" />

> 参考: [OpenAIのGPT-4oを日本語OCRとして使ってみる](https://zenn.dev/tomioka/articles/74adf0c6bc8bc6)

### 2-4. OpenAIノードに設定します。

OpenAIノードの設定にAPIキーを追加します。

[こちらのリスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit?usp=sharing)からOpenAIのAPIキーをコピーします。

OpenAIノードにAPIキーを設定して完了してください。

> <img src="https://i.gyazo.com/e9475922960843c2e95a37aaa7289cd5.png" width="400px" />

### 2-4. 使ってみる

`カメラノード`のボタンを押すと最初は許諾を求められるので許可しましょう。

> <img src="https://i.gyazo.com/dd6bb199d30f2f9d3d5fc8848e6ad512.png" width="400px" />

ボタンを押すと写真が撮影されます。

### 2-3. 上手くいくと

こんな感じで試せます。

> [<img src="https://i.gyazo.com/d32fba58cd0521aecf3fd65a0ef174dd.jpg" width="400px" />](https://twitter.com/n0bisuke/status/1790387951739756841)


## 3. contentの中身がプロンプト

Functionノード内のコードを見てみると`content`という項目に英語で文章が書かれています。

```
You are an Optical Character Recognition (OCR) machine. You will extract all the characters from the image file in the URL provided by the user, and you will only privide the extracted text in your response. As an OCR machine, You can only respond with the extracted text.
```

DeepLで日本語訳をすると

**"あなたは光学式文字認識(OCR)マシンです。あなたはユーザーから提供されたURLの画像ファイルからすべての文字を抽出し、抽出されたテキストのみを回答として公開します。OCRマシンとして、あなたは抽出されたテキストでのみ応答することができます。"**

という内容が書かれていて。写真を読み込んだら文字を抽出するように`GPT-4o`に指示を出しています。

ここの文章（プロンプト）を変えることでOCR以外の挙動もさせることができ、別のアプリを組むことが出来ます。

まずここでは完成されたフローを使ってGPT-4oの一部の機能を試してみましょう。

GPT-4oは文章生成、画像認識、音声認識、など色々な機能がありますが、現時点で外部から（APIで）アクセスできるのは文章と画像認識（Vision）の機能のようです。

1. まずはこちらを自身のNode-RED環境に読み込んでみましょう。

```json
[ { "id": "f4f5bdad28d20988", "type": "camera", "z": "f5ecc406a021ecb1", "name": "", "x": 170, "y": 120, "wires": [ [ "af49c26bcb0af17d", "94791895efac735a" ] ] }, { "id": "af49c26bcb0af17d", "type": "image", "z": "f5ecc406a021ecb1", "name": "", "width": 160, "data": "payload", "dataType": "msg", "thumbnail": false, "active": true, "pass": false, "outputs": 0, "x": 320, "y": 240, "wires": [] }, { "id": "311d1fa30186ae04", "type": "openai", "z": "f5ecc406a021ecb1", "name": "", "api": "", "creds": "1602917191132554", "x": 630, "y": 200, "wires": [ [ "c60fa916870c2524" ] ] }, { "id": "94791895efac735a", "type": "base64", "z": "f5ecc406a021ecb1", "name": "", "action": "", "property": "payload", "x": 340, "y": 140, "wires": [ [ "a771ddf4203e4ac7", "370a138f92dc50f1" ] ] }, { "id": "a771ddf4203e4ac7", "type": "function", "z": "f5ecc406a021ecb1", "name": "function 3", "func": "msg.api = 'chat/completions';\nmsg.params = {\n    model: \"gpt-4o\",\n    max_tokens: 1024,\n    messages: [\n      {\n        role: \"system\",\n        content: \"You are an Optical Character Recognition (OCR) machine. You will extract all the characters from the image file in the URL provided by the user, and you will only privide the extracted text in your response. As an OCR machine, You can only respond with the extracted text.\"\n      },\n      {\n        role: \"user\",\n        content: [\n          { type: \"text\", text: \"Please extract all characters within the image. Return the only extacted characters.\" },\n          {\n            type: \"image_url\",\n            image_url: {\n              \"url\": `data:image/jpeg;base64,${msg.payload}`\n            },\n          },\n        ],\n      },\n    ],\n  }\nreturn msg;", "outputs": 1, "timeout": 0, "noerr": 0, "initialize": "", "finalize": "", "libs": [], "x": 480, "y": 160, "wires": [ [ "311d1fa30186ae04" ] ] }, { "id": "370a138f92dc50f1", "type": "debug", "z": "f5ecc406a021ecb1", "name": "debug 18", "active": true, "tosidebar": true, "console": false, "tostatus": false, "complete": "false", "statusVal": "", "statusType": "auto", "x": 760, "y": 300, "wires": [] }, { "id": "c60fa916870c2524", "type": "change", "z": "f5ecc406a021ecb1", "name": "", "rules": [ { "t": "set", "p": "payload", "pt": "msg", "to": "payload.choices[0].message.content", "tot": "msg" } ], "action": "", "property": "", "from": "", "to": "", "reg": false, "x": 700, "y": 240, "wires": [ [ "370a138f92dc50f1" ] ] }, { "id": "1602917191132554", "type": "openaiApiKey", "name": "" } ]
```

2. 次に[こちらのリスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit?usp=sharing)からOpenAIのAPIキーをコピーします。

3. OpenAIノードに設定します。

### 2-2. 使ってみる

`カメラノード`のボタンを押すと最初は許諾を求められるので許可しましょう。

> <img src="https://i.gyazo.com/dd6bb199d30f2f9d3d5fc8848e6ad512.png" width="400px" />

ボタンを押すと写真が撮影されます。

### 2-3. 上手くいくと

こんな感じで試せます。

> [<img src="https://i.gyazo.com/d32fba58cd0521aecf3fd65a0ef174dd.jpg" width="400px" />](https://twitter.com/n0bisuke/status/1790387951739756841)



> [<img src="https://i.gyazo.com/a2782376a5cf2140f89108fa7be4da53.png" width="400px" />
](https://twitter.com/n0bisuke/status/1790391750596436454)

- [おまけ](https://twitter.com/n0bisuke/status/1790392932606046704)

## 2. 

## 3. 世の中のスピードが加速する

昨日はGoogle I/Oがあり、そこでも色々な情報が出ていました。


## 4. 

とはいえ今回の授業ではまずは戦国時代的に話題のLLMを中心に扱っていこうと思います。

---

**[◀ 目次ページに戻る](../readme.md)**
