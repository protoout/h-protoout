# A-1. OpenAIのノードをつかってみよう simple gtpノードでAPIから取得したデータを翻訳


## 1. Node-REDの中にChatGPTを組み込もう！

Node-REDの中でChatGPTを使い、サービスに簡単に生成AIを組み込むことができます。

これにより、ニュースのAPIから取得した情報を要約して送信したり、人間らしい反応を返すチャットボットを作ったり、さまざまなことが可能になります。

OpenAIのノード（[OpenAI API](https://openai.com/index/openai-api/)をNode-REDで簡単に扱えるノード）を使い、Node-REDのフローに生成AIを組み込んでAPIで取得した文章を日本語に翻訳してみましょう！


## 2.やってみよう

### 1-0 タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

[停止用ノードはこちら](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)



準備ができたら早速始めていきます！


### 1-1 NASAのAPIの情報を取得するところまで作る

1. NASA APIの情報取得ができるようにする

[2. 外部サービス連携や情報取得をしてみよう② APIを使って情報取得](../lesson02-api/02_nasa.md)の`### 2. 手順`まで行って、データが返ってくるところまで作成してください。

<img src="https://i.gyazo.com/17a02c204783ee4adf59112b942f4be1.png" alt="Image Description" width="500"/>

または、下記をNode-REDで読み込んでください。

■ 読み込み用JSONはこちら

※ http requestノードのURL後ろ、APIキーを書き換えるのを忘れずに！

APIキーは[こちらの資料](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「NASA API」のキーを入力してください。

```json

[{"id":"45edf3530a1ccca6","type":"inject","z":"2e35bc2966601a96","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":120,"y":80,"wires":[["c7fc2eaae4424f10"]]},{"id":"c7fc2eaae4424f10","type":"http request","z":"2e35bc2966601a96","name":"","method":"GET","ret":"obj","paytoqs":"ignore","url":"https://api.nasa.gov/planetary/apod?api_key=【APIキー】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":310,"y":80,"wires":[["9d1ecf939443eef7"]]},{"id":"9d1ecf939443eef7","type":"debug","z":"2e35bc2966601a96","name":"debug 19","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":500,"y":80,"wires":[]}]

```


### 1-1 Node-REDにsimple-chatgptのノードをインストールする

1. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

2. 「ノードを追加」をクリックし、ノードの名前で検索してください。

**インポートするノードはこれ**
   - [node-red-contrib-simple-chatgpt](https://flows.nodered.org/node/node-red-contrib-simple-chatgpt)


3. 同じ名前のノードを見つけたら「ノードを追加」をクリックしてください。

### 1-2 simple-chatgptノードを使ってみよう

4つのノードを置き、図のようにつなぎます。

- inject
- change
- simple-chatgpt
- debug

<a href="https://gyazo.com/99680f7ab8c4b42eb871dea41c7d01c6"><img src="https://i.gyazo.com/99680f7ab8c4b42eb871dea41c7d01c6.gif" alt="Image from Gyazo" width="600"/></a>


changeとsimple-chatgptをこのように設定してください。
simple-chatgptはAPIキーを入力します。
[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。

<a href="https://gyazo.com/2770b4714ff7000ac78114bc2d2df896"><img src="https://i.gyazo.com/2770b4714ff7000ac78114bc2d2df896.gif" alt="Image from Gyazo" width="600"/></a>


デプロイして、injectのボタンをクリックし、ChatGPTから返答があれば成功です！
<a href="https://gyazo.com/2340a26edf8451c86594e43281c620dc"><img src="https://i.gyazo.com/2340a26edf8451c86594e43281c620dc.png" alt="Image from Gyazo" width="1287"/></a>


### 1-3 simple-chatgptノードでNASA APIの文章を翻訳する

では、今まで作ったフローをつなげて、NASA APIの情報を日本語にしてみましょう！

1. 試しにNASA APIのレスポンスとsimple-chatgptをつなげてみる

<a href="https://gyazo.com/285e7d3b8c9c6264d9183132fa6acd58"><img src="https://i.gyazo.com/285e7d3b8c9c6264d9183132fa6acd58.png" alt="Image from Gyazo" width="500"/></a>

エラーが出ました。

```
"400, "Invalid type for 'messages[0].content': expected one of a string or array of objects, but got an object instead.""

```

「データの型が無効です。文字列または配列は受け付けてるけど、そうじゃないものが来ました。」

と、言っています。

APIから送られてきたJSONデータそのままは受け付けないようです。


2. templateノードを入れて図のように設定

<a href="https://gyazo.com/c887e59783abb098f19af7c7a6c3e9b4"><img src="https://i.gyazo.com/c887e59783abb098f19af7c7a6c3e9b4.gif" alt="Image from Gyazo" width="600"/></a>

※同様のことはchangeノードでもできますが、この後翻訳してもらうプロンプトをいれるのでtemplateノードを使います。


- templateの中身

```
{{payload.explanation}}

```

★ おさらい: NASA APIのレスポンスの構造は、`explanation`にテキスト、`url`の中に画像のURLが含まれています。
そのため、テキスト部分のみを取り出すのに`payload.explanation`を入力しています。

[JSONデータの取り扱いについて](/tools/json-data.md)はこちら


```json
{"copyright":"Sergio Eguivar",
"date":"2024-05-14",
"explanation":"For the mostly harmless denizens of planet Earth, the brighter stars of open cluster NGC 2169 seem to form a cosmic 37. Did you expect 42? From our perspective, the improbable numerical asterism appears solely by chance. It lies at an estimated distance of 3,300 light-years toward the constellation Orion. As far as galactic or open star clusters go, NGC 2169 is a small one, spanning about 7 light-years.  Formed at the same time from the same cloud of dust and gas, the stars of NGC 2169 are only about 11 million years old. Such clusters are expected to disperse over time as they encounter other stars, interstellar clouds, and experience gravitational tides while hitchhiking through the galaxy. Over four billion years ago, our own Sun was likely formed in a similar open cluster of stars.   Gallery: Earth Aurora from Solar Active Region 3664",
"hdurl":"https://apod.nasa.gov/apod/image/2405/NGC2169LRGBQHY183HR.jpg","media_type":"image","service_version":"v1",
"title":"The 37 Cluster",
"url":"https://apod.nasa.gov/apod/image/2405/NGC2169LRGBQHY183HR_c1024.jpg"}
```

3. 試してみる
NASA APIノードにつながっているinjectをクリックして、何かしらChatGPTから返答があれば成功です。

<a href="https://gyazo.com/180602272ae846e9b85216847db6d53d"><img src="https://i.gyazo.com/180602272ae846e9b85216847db6d53d.png" alt="Image from Gyazo" width="337"/></a>

送ったテキスト情報に対して、ChatGPTが適当にコメントしています。


4. templateノードのプロンプトを書き足す

翻訳してほしいので、templateノードのプロンプトを書き足しましょう。

templateノードの中身

```
次の文章を日本語に翻訳してください
{{payload.explanation}}

```

5. 試してみる

もう一度NASA APIノードにつながっているinjectをクリックして、日本語に翻訳された文章が返ってくれば成功です！

<a href="https://gyazo.com/98b155f5148d662a79eb1fe7ee7fe075"><img src="https://i.gyazo.com/98b155f5148d662a79eb1fe7ee7fe075.png" alt="Image from Gyazo" width="337"/></a>


6. プロンプトを変えてみよう

他にも、要約や、英語と日本語を併記させるなど、プロンプトを変更してどのような出力が得られるか試してみましょう！


完成したフローは以下。

※APIキー等は自分で入れてください

```JSON
[{"id":"e5ce054a849ab482","type":"inject","z":"2e35bc2966601a96","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":120,"y":260,"wires":[["96467f0d9dfe631e"]]},{"id":"96467f0d9dfe631e","type":"change","z":"2e35bc2966601a96","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"こんにちは〜〜","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":300,"y":260,"wires":[["fb8c0d4bcc23f5c7"]]},{"id":"af610739720244cb","type":"debug","z":"2e35bc2966601a96","name":"debug 18","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":680,"y":260,"wires":[]},{"id":"fb8c0d4bcc23f5c7","type":"simple-chatgpt","z":"2e35bc2966601a96","name":"","Token":"【OpenAI APIキー】","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":520,"y":260,"wires":[["af610739720244cb"]]},{"id":"45edf3530a1ccca6","type":"inject","z":"2e35bc2966601a96","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":120,"y":80,"wires":[["c7fc2eaae4424f10"]]},{"id":"c7fc2eaae4424f10","type":"http request","z":"2e35bc2966601a96","name":"","method":"GET","ret":"obj","paytoqs":"ignore","url":"https://api.nasa.gov/planetary/apod?api_key=【NASA API キー】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":310,"y":80,"wires":[["9d1ecf939443eef7","4bf97be4f7e96fca"]]},{"id":"9d1ecf939443eef7","type":"debug","z":"2e35bc2966601a96","name":"debug 19","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":500,"y":80,"wires":[]},{"id":"4bf97be4f7e96fca","type":"template","z":"2e35bc2966601a96","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"次の文章を日本語に翻訳してください\n{{payload.explanation}}","output":"str","x":400,"y":160,"wires":[["fb8c0d4bcc23f5c7"]]}]

```

---

**[◀ 目次ページに戻る](../readme.md)**