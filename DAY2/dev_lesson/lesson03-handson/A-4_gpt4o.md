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

### 2-4. OpenAIノードにAPIキーを設定

OpenAIノードの設定にAPIキーを追加します。

[こちらのリスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit?usp=sharing)からOpenAIのAPIキーをコピーします。

OpenAIノードにAPIキーを設定して完了してください。

> <img src="https://i.gyazo.com/e9475922960843c2e95a37aaa7289cd5.png" width="400px" />

### 2-5. 使ってみる

ここまでで設定完了です。デプロイして実行してみます。

`カメラノード`のボタンを押すと最初は許諾を求められるので許可しましょう。

> <img src="https://i.gyazo.com/dd6bb199d30f2f9d3d5fc8848e6ad512.png" width="400px" />

ボタンを押すと写真が撮影されます。

### 2-6. 上手くいくと

こんな感じで試せます。

> [<img src="https://i.gyazo.com/d32fba58cd0521aecf3fd65a0ef174dd.jpg" width="400px" />](https://twitter.com/n0bisuke/status/1790387951739756841)

出来上がったものは最初に試したものと同様ですね。

## 3. プロンプトを変えると別のアプリに

Functionノード内のコードを見てみると`content`という項目に英語で文章が書かれています。

この`content`の中身がプロンプトになっています。

```
You are an Optical Character Recognition (OCR) machine. You will extract all the characters from the image file in the URL provided by the user, and you will only privide the extracted text in your response. As an OCR machine, You can only respond with the extracted text.
```

DeepLで日本語訳をすると

**"あなたは光学式文字認識(OCR)マシンです。あなたはユーザーから提供されたURLの画像ファイルからすべての文字を抽出し、抽出されたテキストのみを回答として公開します。OCRマシンとして、あなたは抽出されたテキストでのみ応答することができます。"**

という内容が書かれていて。写真を読み込んだら文字を抽出するように`GPT-4o`に指示を出しています。

ここの文章（プロンプト）を変えることでOCR以外の挙動もさせることができ、別のアプリを組むことが出来ます。

## 4. 応用を考える

文字以外にも写真から抽出できる情報はたくさんあるので例えば以下のような`パーソナルドクターアプリ`も作れそうです。

```
あなたはパーソナルドクターです。
あなたはユーザーから提供されたURLの画像ファイルから顔を読み取り、顔の状態からユーザーの健康状態を読み取り、顔の状態から読み取れる健康状態をユーザーにフィードバックしてあげてください。

顔が読み取れない時は再度画像を送るように促してください。
```

> ChatGPTで試すとこのように動作するので↑のプロンプトで十分それっぽい挙動をしてくれます。
> 
> <img src="https://i.gyazo.com/38b311265ece1deb45a6e64a9c57681e.png" width="400px" />
> 
> <img src="https://i.gyazo.com/19b1fff02731437f651cd14e9f49e6ef.png" width="400px" />

肌が乾燥してるしクマがあるしって言われてます。合ってます。優秀ですね。

このような形で優秀なAIを使って何ができるか少し考えてみましょう。

---

**[◀ 目次ページに戻る](../readme.md)**
