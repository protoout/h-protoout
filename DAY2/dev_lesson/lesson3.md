### OpenAIのノードをつかってみよう

今度は、OopenAIのノードをを使い、Node-REDのフローに生成AIを組み込んでみましょう！


## 音声でLEDを操作するものを作ります！
完成イメージは以下。

「電気つけて」というとLEDが光ります。

「光らせて」「ただいま」「もう出かける」など、曖昧な表現でもLEDを光らせたり消したりしてくれます。




[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)



## やってみよう

### 1-0 タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

停止用ノードは下記。
```json
[{"id":"cb1d6d3a.017e1","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":610,"y":140,"wires":[]},{"id":"11a346f0.5a4c19","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"msg.payload = \"finish\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":440,"y":140,"wires":[["cb1d6d3a.017e1"]]},{"id":"76e43759.3dff68","type":"inject","z":"d9dba4a1.01f228","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":260,"y":140,"wires":[["11a346f0.5a4c19"]]}]
```

▼読み込み結果  
<a href="https://gyazo.com/ac38f368a5f4fefc730b30c4b6984944"><img src="https://i.gyazo.com/ac38f368a5f4fefc730b30c4b6984944.png" alt="Image from Gyazo" width="579"/></a>


準備ができたら早速始めていきます！



### 1-1 Node-REDに3つのノードをインストールする


- node-red-contrib-simple-chatgpt
- node-red-contrib-simple-whisper
- node-red-node-ui-microphone

<details><summary>【1日目のおさらい】ノードをインストールする方法</summary>

1. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

2. 「ノードを追加」をクリックし、ノードの名前で検索してください。

**インポートするノードはこの3つ**
   - node-red-contrib-simple-chatgpt
   - node-red-contrib-simple-whisper
   - node-red-node-ui-microphone

   <a href="https://gyazo.com/44977736c5df5749bfeb4102fc7e1d37"><img src="https://i.gyazo.com/44977736c5df5749bfeb4102fc7e1d37.png" alt="Image from Gyazo" width="800"/></a>

3. 同じ名前のノードを見つけたら「ノードを追加」をクリックしてください。

</details>


### 1-2 話した言葉を文字列に変換するパートをつくる

1. ノードの配置: 左のノードパレットから3つのノードを配置し、図のようにつなげてください。

- microphoneノード
- simple-whisperノード
- debugノード


<img src="https://i.gyazo.com/6a9bdd0f3c5baed80e339774248b8899.png" width="500px">


2. simple-whisperノードの設定: simple-whisperノードをダブルクリックし、API Keyを挿入します。

[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。

<img src="https://i.gyazo.com/83b97c4bfe81e4ee96c6112858d943d3.png" width="500px">


3. microphoneノードの設定: microphoneノードをダブルクリックし下記の様に設定を行います。

- グループ: Home Default
- モード: オーディオ入力

<img src="https://i.gyazo.com/67450db29e6d78119f5da3b73e1e7493.png" alt="Image from Example" width="500px">


4. 「デプロイ」をクリックしてください

5. テスト: マイクから入力した音声がテキストに変換できるか試してみましょう

<img src="https://i.gyazo.com/fa774125e0f067adb6c40a7adae38a11.gif" alt="Image from Example" width="500px">



### 1-3 simple-chatgptノードでLEDを光らせられるようにする

1. 下記、4つのノードを配置し図のようにつなげる
- injectノード
- simple-chatgptノード
- debugノード
- obniz functionノード

<img src="https://i.gyazo.com/2bb0475660f4821f9323888a0ccaa3c7.png" alt="Image from Gyazo" width="579"/>


2. injectノードの設定を変更

「タイムスタンプ」を **「文字列」** に変更してください。

<img src="https://i.gyazo.com/943db55065302edcd00f4e6caef03dd8.png" alt="Image Description" width="500px">



図のフォームに、プロンプトをコピーして貼り付けてください。

<img src="https://i.gyazo.com/6fc3c9bbf078c0c175e352a37b5989d4.png" alt="Image from Gyazo" />


プロンプト
``` 
あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」

```


3. simple-chatgptノードの設定

ダブルクリックしてAPIキーを入力します。
[授業で使う情報リスト](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「OpenAI」行の「keyなど」にある`sk-`で始まる文字列をコピーして貼り付けてください。wisperに入力したものと同じ文字列です。

<img src="https://i.gyazo.com/21751ab4a6842fffb3bb736ea7f54a16.png" alt="Image Description" />


4. obniz functionノードの設定


obniz functionノードをダブルクリックし、obnizを選択してコードを入力します。

<img src="https://i.gyazo.com/4ec524cf0e8e72c28ecdfd43a1fcfda0.png" alt="Image Description" />


```javascript

if (msg.payload == "on") {
    obnizParts.led.on();
} else {
    obnizParts.led.off();
}

```


さらに、obnizの初期コードを追加します。


鉛筆マークをクリックし

<img src="https://i.gyazo.com/7c5951f1e91dc03196fc008d660746bc.png" alt="Image from Gyazo" />

下記1行を追加してください。

```js
obnizParts.led = obniz.wired("LED", {anode:0, cathode:1});

```

<img src="https://i.gyazo.com/efcbc666883c3de9d6cfa03269686431.png" alt="Image from Gyazo" />

あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」


5. LEDをobnizに差し込む

<a href="https://gyazo.com/98db436f266ccce9fe822ccb64b63087"><img src="https://i.gyazo.com/98db436f266ccce9fe822ccb64b63087.png" alt="Image from Gyazo" width="1000"/></a>

- LEDの長い脚をobnizの0番
- LEDの短い脚をobnizの1番

に接続してください。


6. LEDがつくか、テストしましょう

デプロイしてobnizの電源を入れてください。

その後、injectノードのボタンをクリックしてLEDが点灯しコンソールに「on」と出力されるか確かめてください。

<img src="https://i.gyazo.com/73f5121b9021d7aa5961e51af50643d2.png" alt="Image from Gyazo" />



### 1-4 音声入力でLEDを光らせるようにフローをつなげる

さあ、いよいよ最後の工程です！

先ほど作成した、話した言葉を文字列に変換するフローと、命令文にしたがってLEDを点灯するフローをつなげます。


1. templeteノードを追加し、図のように接続する

<img src="https://i.gyazo.com/06898b6a85e4242a63eaa35cd72caaa5.png" alt="Image from Gyazo" />


2. templeteノードを編集する
templeteノードのに下記プロンプトをコピペしてください。

<img src="https://i.gyazo.com/e6cc7a1a0f3447403c8bc500961272f5.png" alt="Image from Gyazo" />

```
あなたは、電気を操作するbotです。
電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出力しないでください。 

# 命令:  {{payload}} !

```

これで完成です！


早速、デプロイして試してみましょう。


[![完成イメージ](https://i.gyazo.com/36c027b8c9afe9318cfb8cb0ec064941.jpg)](https://www.canva.com/design/DAGDMT1WZ7Y/XYLYKHGyz5rJhG01yP1LEQ/watch?utm_content=DAGDMT1WZ7Y&utm_campaign=designshare&utm_medium=embeds&utm_source=link)



### 完成したノード
```JSON
[{"id":"e0554e98e384102c","type":"ui_microphone","z":"922cab1da68a7d27","name":"","group":"4a03c246.55f3d8","order":5,"width":0,"height":0,"maxLength":5,"maxRecogLength":5,"timeslice":0,"press":"click","mode":"audio","interimResults":false,"x":189.99998474121094,"y":542.8571281433105,"wires":[["8eef37912da56e6e"]]},{"id":"d3d1a155253ea60d","type":"debug","z":"922cab1da68a7d27","name":"debug 13","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":669.9999847412109,"y":562.8571281433105,"wires":[]},{"id":"8eef37912da56e6e","type":"simple-whisper","z":"922cab1da68a7d27","name":"","Token":"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","extension":"wav","x":399.99998474121094,"y":562.8571281433105,"wires":[["d3d1a155253ea60d","c96229a2cb5dca4d"]]},{"id":"3577e7991d500933","type":"inject","z":"922cab1da68a7d27","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"あなたは、電気を操作するbotです。電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出しないでください。 # 命令 「電気つけて欲しい」","payloadType":"str","x":210,"y":780,"wires":[["4396d322d17742d0"]]},{"id":"73fc4242956b514a","type":"debug","z":"922cab1da68a7d27","name":"debug 10","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":699.9999847412109,"y":802.8571281433105,"wires":[]},{"id":"bc2ca3e134ce8e7d","type":"obniz-function","z":"922cab1da68a7d27","obniz":"a5fae3ca0b96e551","name":"LED","code":"\nif(msg.payload == \"on\"){\n    obnizParts.led.on();\n}else{\n    obnizParts.led.off();\n}","x":690,"y":880,"wires":[[]]},{"id":"4396d322d17742d0","type":"simple-chatgpt","z":"922cab1da68a7d27","name":"","Token":"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","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":499.99998474121094,"y":802.8571281433105,"wires":[["73fc4242956b514a","bc2ca3e134ce8e7d"]]},{"id":"c96229a2cb5dca4d","type":"template","z":"922cab1da68a7d27","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"あなたは、電気を操作するbotです。\n電気をつけてほしそうな場合は「on」と出力し、消してほしそうなときは「off」と出力してください。on/off以外の言葉は出力しないでください。 \n\n# 命令:  {{payload}} !","output":"str","x":440,"y":700,"wires":[["4396d322d17742d0"]]},{"id":"4a03c246.55f3d8","type":"ui_group","name":"Default","tab":"ccec3682.947098","order":1,"disp":true,"width":"6","collapse":false},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"","accessToken":"","code":"obniz.display.clear(); // 画面を消去\nobniz.display.print(\"Git Hub codespace\");\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});"},{"id":"ccec3682.947098","type":"ui_tab","name":"Home","icon":"dashboard","order":1}]


```

