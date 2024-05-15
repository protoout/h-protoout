### 2. OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する


## 音声でLEDを操作するものを作ります！
完成イメージは以下。

「電気つけて」というとLEDが光ります。

「光らせて」「ただいま」「もう出かける」など、曖昧な表現でもLEDを光らせたり消したりしてくれます。


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)

## はじめる前に

<span style="color:red;">※ このハンズオンではPCのマイクを使用します。Node-REDの環境によりできないことがありますので最初にマイクが使えるか確かめてください。<span>

利用可能なNode-RED

OKな例: ブラウザのURLバー左に鍵マークがついている

<a href="https://gyazo.com/a8a6a8620c51ab73074bbf27457d96dc"><img src="https://i.gyazo.com/a8a6a8620c51ab73074bbf27457d96dc.png" alt="Image from Gyazo" width="316"/></a>

NGな例: ブラウザのURLバー左に「セキュリティ保護なし」と表示がある

<a href="https://gyazo.com/f0614411747abc4daca5461978fac662"><img src="https://i.gyazo.com/f0614411747abc4daca5461978fac662.png" alt="Image from Gyazo" width="310"/></a>

→ セキュリティ保護なしとある場合は、近くのTAに声をかけてNode-RED環境を変更してください。


1. ノードをインストール
- `node-red-contrib-browser-utils`

<a href="https://gyazo.com/d6b1199c411d9b650d8c787d5dbc4a63"><img src="https://i.gyazo.com/d6b1199c411d9b650d8c787d5dbc4a63.gif" alt="Image from Gyazo" width="600"/></a>

2. ノードを配置

- microphone
- debug

<a href="https://gyazo.com/91e5086f34eb83504e519a0cceeea3dc"><img src="https://i.gyazo.com/91e5086f34eb83504e519a0cceeea3dc.gif" alt="Image from Gyazo" width="600"/></a>

2. マイクのテスト

デプロイ後、動作テストしてください。
microphoneノードの左にあるボタンをクリックすると録音開始、もう一度クリックすると止まります。
デバッグノードに図のような数字の配列が表示されれば、マイクが正常に動作しています。

<a href="https://gyazo.com/0366a63cbbf92681fb0bd5f1f6059f8e"><img src="https://i.gyazo.com/0366a63cbbf92681fb0bd5f1f6059f8e.gif" alt="Image from Gyazo" width="600"/></a>


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


1. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

2. 「ノードを追加」をクリックし、ノードの名前で検索してください。

**インポートするノードはこの２つ**
   - node-red-contrib-simple-chatgpt
   - node-red-contrib-simple-whisper


3. 同じ名前のノードを見つけたら「ノードを追加」をクリックしてください。



### 1-2 話した言葉を文字列に変換するパートをつくる

1. ノードの配置: 左のノードパレットから1つのノードを配置・設定してください。

- simple-whisperノード

<a href="https://gyazo.com/fb502b1d70602efb0dff8fd4c84277b2"><img src="https://i.gyazo.com/fb502b1d70602efb0dff8fd4c84277b2.gif" alt="Image from Gyazo" width="600"/></a>

[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。

デプロイし、テストしてみましょう。

さきほどは数字の配列が返ってきましたが、今度は、テキストで返ってきました！

<a href="https://gyazo.com/62274f0a096963c4706902079b411f21"><img src="https://i.gyazo.com/62274f0a096963c4706902079b411f21.gif" alt="Image from Gyazo" width="600"/></a>


### 1-3 simple-chatgptノードでLEDを光らせられるようにする

1. 下記、4つのノードを配置し図のようにつなげる
- injectノード
- changeノード
- simple-chatgptノード
- debugノード

<a href="https://gyazo.com/f902d94a55fcebfb066f7fdf4a0bcf3d"><img src="https://i.gyazo.com/f902d94a55fcebfb066f7fdf4a0bcf3d.png" alt="Image from Gyazo" width="600"/></a>



2. changeノードの設定を変更


プロンプト
``` 
あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」

```


3. simple-chatgptノードの設定

ダブルクリックしてAPIキーを入力します。
[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。wisperに入力したものと同じ文字列です。


4. 動作をテストする

ここまで来たら、一度動作のテストをしましょう。

デプロイしたあと、injectノードをクリックすると「on」と返ってくることを確かめてください。

<a href="https://gyazo.com/f902d94a55fcebfb066f7fdf4a0bcf3d"><img src="https://i.gyazo.com/f902d94a55fcebfb066f7fdf4a0bcf3d.png" alt="Image from Gyazo" width="600"/></a>


4. LEDを光らせるobnizのノードを置く

パーツマニュアルより[LED](/tools/parts-manual/Indicator/led.md)を開いて、injectノードの操作によりLEDのON/OFF
ができるところまで作成してください。


5. 確認

このように、大きく3つのフローができていればOKです。

<a href="https://gyazo.com/9877bdc8218af976d4b22555e32b15c2"><img src="https://i.gyazo.com/9877bdc8218af976d4b22555e32b15c2.png" alt="Image from Gyazo" width="500"/></a>

わからなくなっちゃった人向け:

#### セーブポイント
Node-REDから読み込みをすると追いつけます

```json
[{"id":"cce0567a24e44e5e","type":"debug","z":"0373d611e7a78a5d","name":"debug 14","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":700,"y":60,"wires":[]},{"id":"dd081bb6d6edf4ab","type":"microphone","z":"0373d611e7a78a5d","name":"","x":290,"y":40,"wires":[["575bb9c6b5e25e45"]]},{"id":"575bb9c6b5e25e45","type":"simple-whisper","z":"0373d611e7a78a5d","name":"","Token":"sk-proj-iQYLaB7zvt2qZMhGY0vET3BlbkFJCBMaUTnVwitXZQ88bZoc","extension":"wav","x":480,"y":60,"wires":[["cce0567a24e44e5e"]]},{"id":"67854e1564ef0eb3","type":"inject","z":"0373d611e7a78a5d","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":180,"y":180,"wires":[["35e20b4fe971279a"]]},{"id":"c5b7f5896a1eb3bf","type":"debug","z":"0373d611e7a78a5d","name":"debug 15","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":720,"y":240,"wires":[]},{"id":"35e20b4fe971279a","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":340,"y":220,"wires":[["4d3bb869619b6059"]]},{"id":"4d3bb869619b6059","type":"simple-chatgpt","z":"0373d611e7a78a5d","name":"","Token":"sk-proj-iQYLaB7zvt2qZMhGY0vET3BlbkFJCBMaUTnVwitXZQ88bZoc","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":540,"y":300,"wires":[["c5b7f5896a1eb3bf"]]},{"id":"85c2eaedcc9a81a2","type":"inject","z":"0373d611e7a78a5d","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":480,"wires":[["0199808c713f771c"]]},{"id":"0199808c713f771c","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":480,"wires":[["8096917daef56b97"]]},{"id":"8096917daef56b97","type":"switch","z":"0373d611e7a78a5d","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":480,"wires":[["ba84a3f2a6d1a59e"],["52045ee0375a49c7"]]},{"id":"ba84a3f2a6d1a59e","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":760,"y":420,"wires":[[]]},{"id":"fcf18145d9dd1b79","type":"inject","z":"0373d611e7a78a5d","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":620,"wires":[["a2047e12ffc9aee1"]]},{"id":"a2047e12ffc9aee1","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":620,"wires":[["8096917daef56b97"]]},{"id":"52045ee0375a49c7","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":780,"y":520,"wires":[[]]},{"id":"3472cad0127105a4","type":"comment","z":"0373d611e7a78a5d","name":"音声を文字列にする","info":"","x":90,"y":40,"wires":[]},{"id":"2ed511c7c5598ef6","type":"comment","z":"0373d611e7a78a5d","name":"LEDをつけるか消すかChatGPTに意味をくみとってもらう","info":"","x":210,"y":140,"wires":[]},{"id":"cbd9f69da08b6df6","type":"comment","z":"0373d611e7a78a5d","name":"LEDのON/OFF","info":"","x":80,"y":420,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"","accessToken":"LU9lVJcNb47aDtOxRk5pPlPCxeiA5ServT8g20LtCOeeEtM2mmgcgqNUglK9gvvo","code":"//obniz.display.clear(); // 画面を消去\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});"}]

```


### 1-4 音声入力でLEDを光らせるようにフローをつなげる

さあ、いよいよ最後の工程です！

先ほど作成した、話した言葉を文字列に変換するフローと、テキストからLEDをONにするかOFFにするか意味を汲み取るフロー、LEDを実際に光らせるフローをつなげます。

1. テキストからLEDをONにするかOFFにするか意味を汲み取るフローと、LEDを実際に光らせるフローをつなげます。

simple gptとswitchをつなぐだけです。

<a href="https://gyazo.com/7da054d41db36189190701c926f85056"><img src="https://i.gyazo.com/7da054d41db36189190701c926f85056.gif" alt="Image from Gyazo" width="500"/></a>



2. 話した言葉を文字列に変換するフローと、テキストからLEDをONにするかOFFにするか意味を汲み取るフローをつなげます。


- templeteノードを追加し、図のように接続し、templateノードを編集してください

<a href="https://gyazo.com/6fdb3c80a1d0900fdd612fafcfced0cd"><img src="https://i.gyazo.com/6fdb3c80a1d0900fdd612fafcfced0cd.gif" alt="Image from Gyazo" width="1000"/></a>


■ プロンプト

```
あなたは、電気を操作するbotです。
電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出力しないでください。 

# 命令:  {{payload}} !

```

payloadの部分には、実際に話した言葉が入ります。


これで完成です！


早速、デプロイして試してみましょう。


直接的な命令だけでなく、「LEDをつけてほしいかもしれない」「ただいま〜」「はじけようぜ！」など、曖昧な表現で話しかけてChatGPTがどのように判断するか確認してみてください。



[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)



### 完成したフロー
```JSON
[{"id":"cce0567a24e44e5e","type":"debug","z":"0373d611e7a78a5d","name":"debug 14","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":700,"y":60,"wires":[]},{"id":"dd081bb6d6edf4ab","type":"microphone","z":"0373d611e7a78a5d","name":"","x":290,"y":40,"wires":[["575bb9c6b5e25e45"]]},{"id":"575bb9c6b5e25e45","type":"simple-whisper","z":"0373d611e7a78a5d","name":"","Token":"sk-proj-iQYLaB7zvt2qZMhGY0vET3BlbkFJCBMaUTnVwitXZQ88bZoc","extension":"wav","x":480,"y":60,"wires":[["cce0567a24e44e5e","2506236fb5a0fe25"]]},{"id":"67854e1564ef0eb3","type":"inject","z":"0373d611e7a78a5d","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":180,"y":180,"wires":[["35e20b4fe971279a"]]},{"id":"c5b7f5896a1eb3bf","type":"debug","z":"0373d611e7a78a5d","name":"debug 15","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":720,"y":240,"wires":[]},{"id":"35e20b4fe971279a","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":340,"y":220,"wires":[["4d3bb869619b6059"]]},{"id":"4d3bb869619b6059","type":"simple-chatgpt","z":"0373d611e7a78a5d","name":"","Token":"sk-proj-iQYLaB7zvt2qZMhGY0vET3BlbkFJCBMaUTnVwitXZQ88bZoc","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":540,"y":300,"wires":[["c5b7f5896a1eb3bf","8096917daef56b97"]]},{"id":"85c2eaedcc9a81a2","type":"inject","z":"0373d611e7a78a5d","name":"ON","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":480,"wires":[["0199808c713f771c"]]},{"id":"0199808c713f771c","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"on","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":480,"wires":[["8096917daef56b97"]]},{"id":"8096917daef56b97","type":"switch","z":"0373d611e7a78a5d","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"on","vt":"str"},{"t":"eq","v":"off","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":550,"y":480,"wires":[["ba84a3f2a6d1a59e"],["52045ee0375a49c7"]]},{"id":"ba84a3f2a6d1a59e","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.on(); //ledをONにする","x":760,"y":420,"wires":[[]]},{"id":"fcf18145d9dd1b79","type":"inject","z":"0373d611e7a78a5d","name":"OFF","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":170,"y":620,"wires":[["a2047e12ffc9aee1"]]},{"id":"a2047e12ffc9aee1","type":"change","z":"0373d611e7a78a5d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"off","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":620,"wires":[["8096917daef56b97"]]},{"id":"52045ee0375a49c7","type":"obniz-function","z":"0373d611e7a78a5d","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.led.off();//ledをOFFにする","x":780,"y":520,"wires":[[]]},{"id":"3472cad0127105a4","type":"comment","z":"0373d611e7a78a5d","name":"音声を文字列にする","info":"","x":90,"y":40,"wires":[]},{"id":"2ed511c7c5598ef6","type":"comment","z":"0373d611e7a78a5d","name":"LEDをつけるか消すかChatGPTに意味をくみとってもらう","info":"","x":210,"y":140,"wires":[]},{"id":"cbd9f69da08b6df6","type":"comment","z":"0373d611e7a78a5d","name":"LEDのON/OFF","info":"","x":80,"y":420,"wires":[]},{"id":"2506236fb5a0fe25","type":"template","z":"0373d611e7a78a5d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"あなたは、電気を操作するbotです。\n電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出力しないでください。 \n\n# 命令:  {{payload}} !","output":"str","x":580,"y":160,"wires":[["4d3bb869619b6059"]]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"","accessToken":"LU9lVJcNb47aDtOxRk5pPlPCxeiA5ServT8g20LtCOeeEtM2mmgcgqNUglK9gvvo","code":"//obniz.display.clear(); // 画面を消去\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});"}]


```


---

**[◀ 目次ページに戻る](./readme.md)**