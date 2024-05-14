### 1. OpenAIのノードをつかってみよう simple gtpノードでAPIから取得したデータを翻訳。加工してみよう

今度は、OopenAIのノード（[OpenAI API](https://openai.com/index/openai-api/)をNode-REDで簡単に扱えるノード）をを使い、Node-REDのフローに生成AIを組み込んでみましょう！


### 1-0 タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

[停止用ノードはこちら](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)



準備ができたら早速始めていきます！




完成したフローは以下。

※APIキー等は自分で入れてください

```JSON

[{"id":"0535e820b3f7b918","type":"inject","z":"cc81042a39216a8c","name":"","props":[{"p":"payload"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":240,"y":720,"wires":[["aef776d15d70c86a"]]},{"id":"aef776d15d70c86a","type":"http request","z":"cc81042a39216a8c","name":"","method":"GET","ret":"obj","paytoqs":"ignore","url":"【NASA API KEY】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":430,"y":720,"wires":[["9cfcad10c9627b23","ec0d7d5880d713b2"]]},{"id":"9cfcad10c9627b23","type":"debug","z":"cc81042a39216a8c","name":"debug 16","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":640,"y":720,"wires":[]},{"id":"828e643c81435daf","type":"http request","z":"cc81042a39216a8c","name":"","method":"POST","ret":"obj","paytoqs":"ignore","url":"【Teams Webhook】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":990,"y":940,"wires":[[]]},{"id":"17037d2a0fff058f","type":"template","z":"cc81042a39216a8c","name":"","field":"payload","fieldType":"msg","format":"json","syntax":"mustache","template":"{\n    \"text\": \"{{payload}}\"\n}","output":"json","x":840,"y":940,"wires":[["828e643c81435daf"]]},{"id":"6f5f56b058a3fbd4","type":"simple-chatgpt","z":"cc81042a39216a8c","name":"","Token":"【OpenAI KEY】","Model":"","SystemSetting":"","functions":"","functionsType":"str","function_call":"auto","function_callType":"str","x":700,"y":840,"wires":[["17037d2a0fff058f","686c73f44aec306e"]]},{"id":"ec0d7d5880d713b2","type":"template","z":"cc81042a39216a8c","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"次の文章を日本語に翻訳して: {{payload.explanation}}","output":"str","x":520,"y":840,"wires":[["6f5f56b058a3fbd4"]]},{"id":"686c73f44aec306e","type":"debug","z":"cc81042a39216a8c","name":"debug 17","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":880,"y":840,"wires":[]}]

```

---

**[◀ 目次ページに戻る](./readme.md)**