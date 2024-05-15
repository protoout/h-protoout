### 2. OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する


## 音声でLEDを操作するものを作ります！
完成イメージは以下。

「電気つけて」というとLEDが光ります。

「光らせて」「ただいま」「もう出かける」など、曖昧な表現でもLEDを光らせたり消したりしてくれます。


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)

## はじめる前に

<span style="color:red;">※ このハンズオンではPCのマイクを使用します。Node-REDの環境によりできないことがありますので最初にマイクが使えるか確かめてください。<span>

1. ノードをインストール

- node-red-contrib-browser-utils

をインストールしてください。

<img src="https://i.gyazo.com/3239a2d14644f8ceabb85272b301fd0a.png" width="500">

<a href="https://gyazo.com/72092e7988133a600204852c2a333556"><img src="https://i.gyazo.com/72092e7988133a600204852c2a333556.png" alt="Image from Gyazo" width="500"/></a>

2. microphoneノードとdebugノードをと配置し、つなげる

<a href="https://gyazo.com/84a2312a7357e62802b00a803036f722"><img src="https://i.gyazo.com/84a2312a7357e62802b00a803036f722.gif" alt="Image from Gyazo" width="500"/></a>

3. デプロイ後、テスト
デプロイし、マイクの許可ポップアップが出たら許可をします。

microphoneノードのボタンを押すと録音開始、もう一度押すと停止します。

停止後、コンソールに数字の配列が返ってくれば成功です。
<a href="https://gyazo.com/c5102182546c53637318b64cd10cd26c"><img src="https://i.gyazo.com/c5102182546c53637318b64cd10cd26c.gif" alt="Image from Gyazo" width="500"/></a>


## やってみよう

### 1-0 タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

[停止用ノードはこちら](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)



準備ができたら早速始めていきます！



### 1-1 Node-REDに2つのノードをインストールする

- node-red-contrib-simple-chatgpt
- node-red-contrib-simple-whisper

1. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

2. 「ノードを追加」をクリックし、ノードの名前で検索してください。

**インポートするノードはこの2つ**
   - node-red-contrib-simple-chatgpt
   - node-red-contrib-simple-whisper


3. 同じ名前のノードを見つけたら「ノードを追加」をクリックしてください。



### 1-2 話した言葉を文字列に変換するパートをつくる

1. simple-wisperノードを追加し設定してください

<a href="https://gyazo.com/0713b48f4f36b4eb29c9e367370a870d"><img src="https://i.gyazo.com/0713b48f4f36b4eb29c9e367370a870d.gif" alt="Image from Gyazo" width="500"/></a>


2. simple-whisperノードの設定: simple-whisperノードをダブルクリックし、API Keyを挿入します。

[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。

<a href="https://gyazo.com/9b4fca14d66b024a134bbc5a800a0a47"><img src="https://i.gyazo.com/9b4fca14d66b024a134bbc5a800a0a47.gif" alt="Image from Gyazo" width="500"/></a>



3. 「デプロイ」をクリックしてください

4. テスト: マイクから入力した音声がテキストに変換できるか試してみましょう

<a href="https://gyazo.com/b2152708177898040b295374b75a83aa"><img src="https://i.gyazo.com/b2152708177898040b295374b75a83aa.gif" alt="Image from Gyazo" width="500"/></a>

配列が、simple-wisperによりテキストに変換されて返ってきました！


### 1-3 simple-chatgptノードを使ってみよう

4つのノードを置き、図のようにつなぎます。

- inject
- change
- simple-chatgpt
- debug

<a href="https://gyazo.com/99680f7ab8c4b42eb871dea41c7d01c6"><img src="https://i.gyazo.com/99680f7ab8c4b42eb871dea41c7d01c6.gif" alt="Image from Gyazo" width="600"/></a>


changeとsimple-chatgptをこのように設定してください。
simple-chatgptはAPIキーを入力します。
[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。wisperに入力したものと同じ文字列です。

<a href="https://gyazo.com/2770b4714ff7000ac78114bc2d2df896"><img src="https://i.gyazo.com/2770b4714ff7000ac78114bc2d2df896.gif" alt="Image from Gyazo" width="600"/></a>


デプロイして、injectのボタンをクリックし、ChatGPTから返答があれば成功です！
<a href="https://gyazo.com/2340a26edf8451c86594e43281c620dc"><img src="https://i.gyazo.com/2340a26edf8451c86594e43281c620dc.png" alt="Image from Gyazo" width="1287"/></a>


### 1-4 simple-chatgptノードに入力するプロンプトを作る

今回は、音声入力した内容をWisperでテキストに変換し、その内容からLEDをONにするべきかOFFにするべきかChatGPTに考えてもらい、「on」または「off」の出力を得ることです。

templateノードを追加し、中にプロンプトを記入してください。

<a href="https://gyazo.com/d52920e2c0586c22d4f982d1fc4dab89"><img src="https://i.gyazo.com/d52920e2c0586c22d4f982d1fc4dab89.gif" alt="Image from Gyazo" width="500"/></a>


プロンプト
``` 
あなたは、電気を操作するbotです。
電気をつけてほしそうな場合は「on」と出力し、
消してほしそうなときは「off」と出力してください。
on/off以外の言葉は出しないでください。 
# 命令  {{payload}}

```

{{payload}}には、simple-wisperからうけとった文字（喋った言葉）が入ります。


ここまで来たら、一度動作のテストをしましょう。


デプロイして、microphoneノードをクリックして言葉を話し、再度microphoneノードをクリックして録音を停止してください。

その後コンソールにonまたはoffと出ることを確認してください。

<a href="https://gyazo.com/4ac1de2099b596bc078ac0fe4652edf1"><img src="https://i.gyazo.com/4ac1de2099b596bc078ac0fe4652edf1.gif" alt="Image from Gyazo" width="500"/></a>



### 1-5. LEDを光らせるobnizのノードを置く

パーツマニュアルより[LED](/tools/parts-manual/Indicator/led.md)を開いて、injectノードの操作によりLEDのON/OFF
ができるところまで作成してください。


5. 確認

このように、大きく3つのフローができていればOKです。

<a href="https://gyazo.com/9877bdc8218af976d4b22555e32b15c2"><img src="https://i.gyazo.com/9877bdc8218af976d4b22555e32b15c2.png" alt="Image from Gyazo" width="500"/></a>

わからなくなっちゃった人向け:

#### セーブポイント
Node-REDから読み込みをすると追いつけます

```json
[{"id":"71c23246d15b1e13","type":"microphone","z":"0373d611e7a78a5d","name":"","x":150,"y":800,"wires":[["692a4b1b6eb45ac2"]]},{"id":"b3bf12f1838c2125","type":"debug","z":"0373d611e7a78a5d","name":"debug 27","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":520,"y":800,"wires":[]},{"id":"692a4b1b6eb45ac2","type":"simple-whisper","z":"0373d611e7a78a5d","name":"","Token":"【API キー】","extension":"wav","x":340,"y":800,"wires":[["b3bf12f1838c2125","f152ecc5234e828b"]]},{"id":"e3b275cd67ab4187","type":"inject","z":"0373d611e7a78a5d","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":160,"y":980,"wires":[["2b0fbe7aa0847fa1"]]},{"id":"77bbf6f0c97a5361","type":"debug","z":"0373d611e7a78a5d","name":"debug 28","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":800,"y":1000,"wires":[]},{"id":"2b0fbe7aa0847fa1","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"こんにちは","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":1000,"wires":[["41f7d09b147e6557"]]},{"id":"41f7d09b147e6557","type":"simple-chatgpt","z":"0373d611e7a78a5d","name":"","Token":"【API キー】","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":620,"y":980,"wires":[["77bbf6f0c97a5361"]]},{"id":"5914cdc18097c8b1","type":"comment","z":"0373d611e7a78a5d","name":"Wisperで音声をテキストにする","info":"","x":130,"y":740,"wires":[]},{"id":"800c635f19219e82","type":"comment","z":"0373d611e7a78a5d","name":"Wisperから受け取った言葉をChatGPTに渡し、内容によってLEDをONまたはOFFにする","info":"","x":310,"y":860,"wires":[]},{"id":"f152ecc5234e828b","type":"template","z":"0373d611e7a78a5d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"あなたは、電気を操作するbotです。\n電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。\non/off以外の言葉は出しないでください。 \n\n# 命令  {{payload}}","output":"str","x":440,"y":900,"wires":[["41f7d09b147e6557"]]},{"id":"7f78c19310429cc1","type":"inject","z":"0373d611e7a78a5d","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1160,"wires":[["128cd3fbed2a036a"]]},{"id":"128cd3fbed2a036a","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1160,"wires":[["1423ee819faf412f"]]},{"id":"1423ee819faf412f","type":"switch","z":"0373d611e7a78a5d","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":1160,"wires":[["25da1a7c5a998ad5"],["ae0af43797b56ef4"]]},{"id":"25da1a7c5a998ad5","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":760,"y":1100,"wires":[[]]},{"id":"8d251288bea4f76a","type":"inject","z":"0373d611e7a78a5d","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1300,"wires":[["362f2e5e501dc5b8"]]},{"id":"362f2e5e501dc5b8","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1300,"wires":[["1423ee819faf412f"]]},{"id":"ae0af43797b56ef4","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":780,"y":1200,"wires":[[]]},{"id":"21e67e5637feb9f3","type":"comment","z":"0373d611e7a78a5d","name":"LEDのON/OFF","info":"","x":80,"y":1100,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"","deviceType":"obnizboard1y","name":"","accessToken":"","code":"//obniz.display.clear(); // 画面を消去\n//obnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});\n\n\n//obnizParts.dht20 = obniz.wired(\"DHT20\",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: \"5v\"}); //0,1,2,3番にピンをアサインし、電圧を5Vに設定\n//obnizParts.light = obniz.wired(\"Keyestudio_TrafficLight\", {gnd:8, green:9, yellow:10, red:11});\n\n//obnizParts.Speaker = obniz.wired(\"Speaker\",{ signal:5, gnd:6 }); \n//obniz.io0.output(true); //io0番を5vに\n//obniz.io2.output(false); //io2番をGNDに\n\n//obnizParts.servo = obniz.wired(\"ServoMotor\",{ signal:3 }); //サーボモーターをどのくらい回すかの信号を2番に設定\nobnizParts.mrfc522 = obniz.wired(\"MFRC522\", { cs: 0, clk: 1, mosi: 2, miso: 3, gnd: 5, rst: 6});"}]

```


### 1-6 音声入力でLEDを光らせるようにフローをつなげる

さあ、いよいよ最後の工程です！

simple-chatgptノードとLEDにつながっているswitchノードを図のようにつなぎます。

<a href="https://gyazo.com/d3cb5d46fafe355c310d09cc2b6e43e9"><img src="https://i.gyazo.com/d3cb5d46fafe355c310d09cc2b6e43e9.gif" alt="Image from Gyazo" width="500"/></a>

これで完成です！

早速、デプロイして試してみましょう。

音声によりLEDをON/OFFできれば成功です！


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)



### 完成したフロー
```JSON
[{"id":"71c23246d15b1e13","type":"microphone","z":"0373d611e7a78a5d","name":"","x":150,"y":800,"wires":[["692a4b1b6eb45ac2"]]},{"id":"b3bf12f1838c2125","type":"debug","z":"0373d611e7a78a5d","name":"debug 27","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":520,"y":800,"wires":[]},{"id":"692a4b1b6eb45ac2","type":"simple-whisper","z":"0373d611e7a78a5d","name":"","Token":"【APIキー】","extension":"wav","x":340,"y":800,"wires":[["b3bf12f1838c2125","f152ecc5234e828b"]]},{"id":"e3b275cd67ab4187","type":"inject","z":"0373d611e7a78a5d","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":160,"y":980,"wires":[["2b0fbe7aa0847fa1"]]},{"id":"77bbf6f0c97a5361","type":"debug","z":"0373d611e7a78a5d","name":"debug 28","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":800,"y":1000,"wires":[]},{"id":"2b0fbe7aa0847fa1","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"こんにちは","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":1000,"wires":[["41f7d09b147e6557"]]},{"id":"41f7d09b147e6557","type":"simple-chatgpt","z":"0373d611e7a78a5d","name":"","Token":"【APIキー】","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":620,"y":980,"wires":[["77bbf6f0c97a5361","1423ee819faf412f"]]},{"id":"5914cdc18097c8b1","type":"comment","z":"0373d611e7a78a5d","name":"Wisperで音声をテキストにする","info":"","x":130,"y":740,"wires":[]},{"id":"800c635f19219e82","type":"comment","z":"0373d611e7a78a5d","name":"Wisperから受け取った言葉をChatGPTに渡し、内容によってLEDをONまたはOFFにする","info":"","x":310,"y":860,"wires":[]},{"id":"f152ecc5234e828b","type":"template","z":"0373d611e7a78a5d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"あなたは、電気を操作するbotです。\n電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。\non/off以外の言葉は出しないでください。 \n\n# 命令  {{payload}}","output":"str","x":440,"y":900,"wires":[["41f7d09b147e6557"]]},{"id":"7f78c19310429cc1","type":"inject","z":"0373d611e7a78a5d","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1160,"wires":[["128cd3fbed2a036a"]]},{"id":"128cd3fbed2a036a","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1160,"wires":[["1423ee819faf412f"]]},{"id":"1423ee819faf412f","type":"switch","z":"0373d611e7a78a5d","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":1160,"wires":[["25da1a7c5a998ad5"],["ae0af43797b56ef4"]]},{"id":"25da1a7c5a998ad5","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":760,"y":1100,"wires":[[]]},{"id":"8d251288bea4f76a","type":"inject","z":"0373d611e7a78a5d","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":1300,"wires":[["362f2e5e501dc5b8"]]},{"id":"362f2e5e501dc5b8","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":1300,"wires":[["1423ee819faf412f"]]},{"id":"ae0af43797b56ef4","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":780,"y":1200,"wires":[[]]},{"id":"21e67e5637feb9f3","type":"comment","z":"0373d611e7a78a5d","name":"LEDのON/OFF","info":"","x":80,"y":1100,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"","deviceType":"obnizboard1y","name":"","accessToken":"","code":"//obniz.display.clear(); // 画面を消去\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});\n\n\n//obnizParts.dht20 = obniz.wired(\"DHT20\",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: \"5v\"}); //0,1,2,3番にピンをアサインし、電圧を5Vに設定\n//obnizParts.light = obniz.wired(\"Keyestudio_TrafficLight\", {gnd:8, green:9, yellow:10, red:11});\n\n//obnizParts.Speaker = obniz.wired(\"Speaker\",{ signal:5, gnd:6 }); \n//obniz.io0.output(true); //io0番を5vに\n//obniz.io2.output(false); //io2番をGNDに\n\n//obnizParts.servo = obniz.wired(\"ServoMotor\",{ signal:3 }); //サーボモーターをどのくらい回すかの信号を2番に設定\n//obnizParts.mrfc522 = obniz.wired(\"MFRC522\", { cs: 0, clk: 1, mosi: 2, miso: 3, gnd: 5, rst: 6});"}]


```


---

**[◀ 目次ページに戻る](./readme.md)**