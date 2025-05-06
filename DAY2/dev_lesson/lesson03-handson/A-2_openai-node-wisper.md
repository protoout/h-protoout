 # 生成 AI のノードを利用してみよう：画像を解析しLEDを操作する


## 1.画像解析の結果を使ってLEDを操作しよう！
引き続き、GitHub Models を使っていきましょう。完成イメージは以下。

電気をつけるアクションを行うとLEDが光ります。

電気をつけるアクションは自分で好きなように決めることができます。


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)

## 3.やってみよう

### 3-2 LED を　On/Off するノード

LED をOn/Offするノードです。なお、[こちらのマニュアル](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/tutorial-led-onoff)を見ながら作成することができます。

■ 読み込み用JSONはこちら

```JSON
[{"id":"9b130ad5dda135a2","type":"inject","z":"60ccb55147cec501","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":230,"y":560,"wires":[["ad4f223f106db94b"]]},{"id":"ad4f223f106db94b","type":"change","z":"60ccb55147cec501","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":440,"y":560,"wires":[["0a65a7c712ad080f"]]},{"id":"0a65a7c712ad080f","type":"switch","z":"60ccb55147cec501","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":610,"y":560,"wires":[["2005153a361e8cd1"],["d9485a0ee1471158"]]},{"id":"2005153a361e8cd1","type":"obniz-function","z":"60ccb55147cec501","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":820,"y":560,"wires":[[]]},{"id":"5f7c57c3309e3209","type":"inject","z":"60ccb55147cec501","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":230,"y":700,"wires":[["2ad4807ef863a8f7"]]},{"id":"2ad4807ef863a8f7","type":"change","z":"60ccb55147cec501","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":440,"y":700,"wires":[["0a65a7c712ad080f"]]},{"id":"d9485a0ee1471158","type":"obniz-function","z":"60ccb55147cec501","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":820,"y":680,"wires":[[]]},{"id":"e6ec6d119e91af6e","type":"comment","z":"60ccb55147cec501","name":"LEDのON/OFF","info":"","x":140,"y":500,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"","deviceType":"obnizboard1y","name":"","accessToken":"","code":" "}]
```

このようになっています。 
![image](https://github.com/user-attachments/assets/73c5fd2b-f4b9-4918-8b7e-60063ee5a9fd)


> [!CAUTION]
> `functionノード`を自身の obniz ID に変更させましょう。
> <img width="484" alt="image" src="https://github.com/user-attachments/assets/1136c08a-e6b2-4dd2-8fc5-c17147c36be7" />

`ON` 、 `OFF` と書かれた`injectノード` を押してみましょう。LED の ON/OFF ができたらOKです！
このフローは`switchノード`で ON/OFF の `obniz functionノード` への分岐を行っています。

<img width="373" alt="image" src="https://github.com/user-attachments/assets/2e5f197c-99ad-4404-b1c4-2bbebc1c9849" />

`ON` の`injectノード`は文字通り`ON` という文字を`switchノード`に受け渡していて、同様に `OFF` の`injectノード`は`OFF` という文字を`switchノード`に受け渡しています。`switchノード`は `ON` という文字列を受け取った時は上の`obniz funcionノード`へ、 `OFF`という文字列を受け取った時は下の`obniz funcionノード`へといった具合です。

<img width="620" alt="image" src="https://github.com/user-attachments/assets/ba4a0640-b0f8-49d3-984b-145a16558143" />


試し終わったら、`obniz-closeノード`で停止しておきましょう。

### 3-2 画像認識を行ってみる

続いて、下記を Node-RED で読み込んでください。

■ 読み込み用JSONはこちら

```JSON
[{"id":"f1af892e1eb6af39","type":"debug","z":"4ff87a6ea45ce30a","name":"debug 2","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":720,"y":500,"wires":[]},{"id":"2c73bd611a0559ea","type":"http request","z":"4ff87a6ea45ce30a","name":"","method":"POST","ret":"obj","paytoqs":"ignore","url":"https://models.inference.ai.azure.com/chat/completions","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":530,"y":420,"wires":[["553a14d9bc4442b6"]]},{"id":"5b90d68cdc3e7216","type":"template","z":"4ff87a6ea45ce30a","name":"image","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"{\n    \"model\": \"gpt-4o\",\n    \"messages\": [\n        {\n            \"role\": \"user\",\n            \"content\": [\n                {\n                    \"type\": \"image_url\",\n                    \"image_url\": {\n                        \"url\": \"data:image/png;base64,{{{payload}}}\"\n                    }\n                },\n                {\n                    \"type\": \"text\",\n                    \"text\": \"日本語で説明してください。\"\n                }\n            ]\n        }\n    ]\n}","output":"json","x":430,"y":340,"wires":[["4916d4c0496da708"]]},{"id":"553a14d9bc4442b6","type":"change","z":"4ff87a6ea45ce30a","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload.choices[0].message.content","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":500,"wires":[["f1af892e1eb6af39"]]},{"id":"0f39b696c5e360ed","type":"base64","z":"4ff87a6ea45ce30a","name":"","action":"","property":"payload","x":280,"y":340,"wires":[["5b90d68cdc3e7216"]]},{"id":"7b362f2050cb454b","type":"camera","z":"4ff87a6ea45ce30a","name":"","x":130,"y":340,"wires":[["18ba713d2039ca81","0f39b696c5e360ed"]]},{"id":"18ba713d2039ca81","type":"image","z":"4ff87a6ea45ce30a","name":"","width":160,"data":"payload","dataType":"msg","thumbnail":false,"active":true,"pass":false,"outputs":0,"x":300,"y":400,"wires":[]},{"id":"4916d4c0496da708","type":"change","z":"4ff87a6ea45ce30a","name":"トークン設定","rules":[{"t":"set","p":"headers.Authorization","pt":"msg","to":"\"Bearer \" & $env(\"GITHUB_TOKEN\")\t","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":600,"y":340,"wires":[["2c73bd611a0559ea"]]},{"id":"7bf142c3efb6786d","type":"comment","z":"4ff87a6ea45ce30a","name":"画像解析を行うフロー","info":"","x":160,"y":280,"wires":[]}]
```

このようになります。

<img width="984" alt="image" src="https://github.com/user-attachments/assets/10b226e5-0edb-4ebc-8ace-40894ec6dc67" />


試しに`cameraノード`を実行してみましょう。
PCのカメラを使って撮影が始まります。ポップアップで許可を求められるので「」を選びましょう。

`image previewノード`の下に撮影した画像が表示されます。
<img width="687" alt="image" src="https://github.com/user-attachments/assets/465ff489-d0c8-4d50-aabe-ef5655e52e63" />

また、右側のサイドバーを虫のマーク(debug)にすると、この画像について解説の解析をしてくれます。
![image](https://github.com/user-attachments/assets/e59fdef4-9291-4b7c-8edb-239c40994441)

これで撮影をするとその画像に関する説明をしてくれるノードができました。細かく内容を見ていきましょう。
読むだけでOKです！

#### base64
画像などのデータを英数字などの文字列に変換するエンコーディング方式(書き替えの手法)です。  
![image](https://github.com/user-attachments/assets/9e9d230d-a1f9-4d91-8bea-f8cc85871ce7)
試しに`Debugノード`に出力させて内容を見てみましょう。

先ほどの画像はこのような文字列になりました。  
<img width="548" alt="image" src="https://github.com/user-attachments/assets/f9d2e13b-8e92-4c0b-918f-e310555d8a15" />

#### 生成 AI にデータを受け渡す部分

この部分ですね。  
<img width="659" alt="image" src="https://github.com/user-attachments/assets/e9724d0e-fe57-482b-a251-3d8d8d5e6977" />

`image` と書かれた`templateノード`には以下の JSON 形式の記述をしています。

先ほどの base64 でつくったデータを`image_url`というデータの型で受け渡し、GPT-4o に「日本語で説明してください。」と伝えています。

```JSON  
{
    "model": "gpt-4o",
    "messages": [
        {
            "role": "user",
            "content": [
                {
                    "type": "image_url",
                    "image_url": {
                        "url": "data:image/png;base64,{{{payload}}}"
                    }
                },
                {
                    "type": "text",
                    "text": "日本語で説明してください。"
                }
            ]
        }
    ]
}
```

このように画像データを一度文字列の形式に変換することで画像データでも扱うことができます。

### 3-3. 2つのフローをつなげて 画像データから LED の ON/OFF を制御しよう

では、今まで作ったフローをつなげてましょう



<a href="https://gyazo.com/d3cb5d46fafe355c310d09cc2b6e43e9"><img src="https://i.gyazo.com/d3cb5d46fafe355c310d09cc2b6e43e9.gif" alt="Image from Gyazo" width="500"/></a>

これで完成です！

早速、デプロイして試してみましょう。

音声によりLEDをON/OFFできれば成功です！


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)



### 完成したフロー
```JSON
[{"id":"71c23246d15b1e13","type":"microphone","z":"0373d611e7a78a5d","name":"","x":150,"y":800,"wires":[["692a4b1b6eb45ac2"]]},{"id":"b3bf12f1838c2125","type":"debug","z":"0373d611e7a78a5d","name":"debug 27","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":520,"y":800,"wires":[]},{"id":"692a4b1b6eb45ac2","type":"simple-whisper","z":"0373d611e7a78a5d","name":"","Token":"【APIキー】","extension":"wav","x":340,"y":800,"wires":[["b3bf12f1838c2125","f152ecc5234e828b"]]},{"id":"e3b275cd67ab4187","type":"inject","z":"0373d611e7a78a5d","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":160,"y":980,"wires":[["2b0fbe7aa0847fa1"]]},{"id":"77bbf6f0c97a5361","type":"debug","z":"0373d611e7a78a5d","name":"debug 28","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":800,"y":1000,"wires":[]},{"id":"2b0fbe7aa0847fa1","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"こんにちは","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":1000,"wires":[["41f7d09b147e6557"]]},{"id":"41f7d09b147e6557","type":"simple-chatgpt","z":"0373d611e7a78a5d","name":"","Token":"【APIキー】","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":620,"y":980,"wires":[["77bbf6f0c97a5361","1423ee819faf412f"]]},{"id":"5914cdc18097c8b1","type":"comment","z":"0373d611e7a78a5d","name":"Wisperで音声をテキストにする","info":"","x":130,"y":740,"wires":[]},{"id":"800c635f19219e82","type":"comment","z":"0373d611e7a78a5d","name":"Wisperから受け取った言葉をChatGPTに渡し、内容によってLEDをONまたはOFFにする","info":"","x":310,"y":860,"wires":[]},{"id":"f152ecc5234e828b","type":"template","z":"0373d611e7a78a5d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"あなたは、電気を操作するbotです。\n電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。\non/off以外の言葉は出しないでください。 \n\n# 命令  {{payload}}","output":"str","x":440,"y":900,"wires":[["41f7d09b147e6557"]]},{"id":"7f78c19310429cc1","type":"inject","z":"0373d611e7a78a5d","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1160,"wires":[["128cd3fbed2a036a"]]},{"id":"128cd3fbed2a036a","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1160,"wires":[["1423ee819faf412f"]]},{"id":"1423ee819faf412f","type":"switch","z":"0373d611e7a78a5d","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":1160,"wires":[["25da1a7c5a998ad5"],["ae0af43797b56ef4"]]},{"id":"25da1a7c5a998ad5","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":760,"y":1100,"wires":[[]]},{"id":"8d251288bea4f76a","type":"inject","z":"0373d611e7a78a5d","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1300,"wires":[["362f2e5e501dc5b8"]]},{"id":"362f2e5e501dc5b8","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1300,"wires":[["1423ee819faf412f"]]},{"id":"ae0af43797b56ef4","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":780,"y":1200,"wires":[[]]},{"id":"21e67e5637feb9f3","type":"comment","z":"0373d611e7a78a5d","name":"LEDのON/OFF","info":"","x":80,"y":1100,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"","deviceType":"obnizboard1y","name":"","accessToken":"","code":"obnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1})"}]


```

---

**[◀ 目次ページに戻る](../readme.md)**
