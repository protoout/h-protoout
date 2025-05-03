> [!CAUTION]
> Github models 実装テスト中
> 
# 生成 AI のノードを利用：テキストを解析し翻訳しよう


## 1. Node-RED の中に ChatGPT を組み込もう！

Node-RED の中で ChatGPT を使い、サービスに簡単に生成AIを組み込むことができます。

これにより、ニュースの API から取得した情報を要約して送信したり、人間らしい反応を返すチャットボットを作ったり、さまざまなことが可能になります。

GitHub Models をNode-REDで簡単に扱えるノード）を使い、Node-RED のフローに生成 AIを組み込んで API で取得した文章を日本語に翻訳してみましょう！

> [!NOTE]
> GitHub Models[^1] は GPT-4o、Llama 3.1、Phi-3、Mistral Large 2などの最新の大規模言語モデル（LLM）を、GitHub上で無料で試すことができます。また、それらのモデルを、簡単にCodespacesに取り込み、コード生成や推論を行うことができます。
> GitHub のアカウントがあれば API キーや複雑な設定なしで、複数の LLM を試すことができるため、今回はこちらから GPT-4o を使っていきます。
> <img width="919" alt="image" src="https://github.com/user-attachments/assets/6ed3779d-2214-471f-ba06-0dddf9319279" />



## 2.やってみよう

### 2-1 NASA の API の情報を取得するところまで作る

NASA API の情報取得ができるようにします。[こちら]()の演習でもやりましたね。

下記を Node-RED で読み込んでください。

■ 読み込み用JSONはこちら

※ http requestノードのURL後ろ、APIキーを書き換えるのを忘れずに！

APIキーは[こちらの資料](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「NASA API」のキーを入力してください。

```json

[{"id":"45edf3530a1ccca6","type":"inject","z":"80cc5966bb5f04f3","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":200,"y":180,"wires":[["c7fc2eaae4424f10"]]},{"id":"c7fc2eaae4424f10","type":"http request","z":"80cc5966bb5f04f3","name":"","method":"GET","ret":"obj","paytoqs":"ignore","url":"https://api.nasa.gov/planetary/apod?api_key=【APIキー】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":390,"y":180,"wires":[["9d1ecf939443eef7"]]},{"id":"9d1ecf939443eef7","type":"debug","z":"80cc5966bb5f04f3","name":"debug 19","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":580,"y":180,"wires":[]},{"id":"1c11b2728bfabc7a","type":"comment","z":"80cc5966bb5f04f3","name":"NASA API (API Key は書きかえてください！)","info":"","x":270,"y":120,"wires":[]}]

```

### 2-2 GPT-4o のノードをインストールする

下記を Node-RED で読み込んでください。

■ 読み込み用JSONはこちら

```JSON
[{"id":"62cd806820605559","type":"debug","z":"4ff87a6ea45ce30a","name":"debug 1","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":620,"y":200,"wires":[]},{"id":"3078eb36016e146b","type":"template","z":"4ff87a6ea45ce30a","name":"text","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"{\n    \"model\": \"gpt-4o\",\n    \"messages\": [\n        {\n            \"role\": \"user\",\n            \"content\": [\n                {\n                    \"type\": \"text\",\n                    \"text\": \"{{{payload}}}\"\n                }\n            ]\n        }\n    ]\n}","output":"json","x":290,"y":120,"wires":[["2e7ddb8620f61517"]]},{"id":"aff805d8e7597301","type":"http request","z":"4ff87a6ea45ce30a","name":"","method":"POST","ret":"obj","paytoqs":"ignore","url":"https://models.inference.ai.azure.com/chat/completions","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":250,"y":200,"wires":[["e98164dd6193cb47"]]},{"id":"e98164dd6193cb47","type":"change","z":"4ff87a6ea45ce30a","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload.choices[0].message.content","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":440,"y":200,"wires":[["62cd806820605559"]]},{"id":"abb7f959c1258ad9","type":"inject","z":"4ff87a6ea45ce30a","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"日立とは","payloadType":"str","x":140,"y":120,"wires":[["3078eb36016e146b"]]},{"id":"2e7ddb8620f61517","type":"change","z":"4ff87a6ea45ce30a","name":"トークン設定","rules":[{"t":"set","p":"headers.Authorization","pt":"msg","to":"\"Bearer \" & $env(\"GITHUB_TOKEN\")\t","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":460,"y":120,"wires":[["aff805d8e7597301"]]},{"id":"87bd5b2f2f6924db","type":"comment","z":"4ff87a6ea45ce30a","name":"GPT-4o","info":"","x":110,"y":60,"wires":[]}]
```

まずは、デプロイして`injectノード`からこちらのフローを実行してみましょう。  
右側のサイドバーを虫のマーク(debug)にすると、「日立とは」という問いに対する GPT-4o の回答を確認できます。生成には5秒ほどかかるかもしれません。  
<img width="450" alt="image" src="https://github.com/user-attachments/assets/129ecb30-eb3d-479a-87dd-259cfdf661c4" />

`inject ノード`のテキストを変えることで、色々な質問ができます。  
<img width="450" alt="image" src="https://github.com/user-attachments/assets/e158433a-9f33-4f01-90b3-90055162d1ce" />


全体では現在このようなフローになっていればOKです！

<img width="450" alt="image" src="https://github.com/user-attachments/assets/a96edfb3-0cf1-4050-9844-e3ca11bc6a79" />



### 2-3 2つのフローをつなげて NASA のデータを翻訳してみよう

では、今まで作ったフローをつなげて、NASA APIの情報を日本語にしてみましょう！

1. 試しに NASA API のレスポンスと GPT-4o をつなげてみる

このように NASA API のレスポンスをそのまま渡してみます。
![image](https://github.com/user-attachments/assets/d8fbc56c-6323-4c69-803e-c61e12786412)


エラーが出ました。

```
"RequestError: read ECONNRESET : https://models.inference.ai.azure.com/chat/completions"

```
これは接続に失敗したということです。データの渡し方が良くなかったです。
はじめは「日立とは」というテキストを渡したのに対し、今回は NASA API のレスポンスで得た JSON をそのまま渡してしまいました。
テキスト形式にして GPT-4o に渡しましょう。
 
2. `templateノード`を入れて図のように設定

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
[^1]: [GitHub Models でどんなモデルが使えるか？](https://github.com/marketplace?type=models)
---

**[◀ 目次ページに戻る](../readme.md)**
