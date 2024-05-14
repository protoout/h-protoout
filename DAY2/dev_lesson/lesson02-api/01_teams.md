# 外部サービス連携や情報取得をしてみよう① Teams編


いつもみなさんが使っているTeamsをWebhookという仕組みを使ってNode-RED経由で連携し、obnizで行った動作をトリガーとしてメッセージを送ってみます。



## 1. obnizのスイッチを押して、Teamsに投稿してみよう

1. injectノード、http requestノード、debugノードを追加し図のようにつなぐ

<img src="https://i.gyazo.com/49636359e2e0c96b19b0ac4f3083ebdd.png" alt="Image Description" width="500"/>

2. http requestノードを図のように設定する。Webhook URLは[こちらの資料](1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs)のteams webhookのURLを入力してください。

<img src="https://i.gyazo.com/6e48aee0cabc082df0fe1242df9e878f.png" alt="Image from Gyazo" width="500"/>

3. obniz repeatノードとtemplateノードを追加し図のようにつなぎます

<img src="https://i.gyazo.com/b4790241510f96649992006763a18e6d.png" alt="Image Description" width="500"/>

4. obniz repeatノードのコードに、下記のコードを貼り付けてください

<img src="https://i.gyazo.com/aa2e7d157119c664f7b2ffb7cb4a8770.png" alt="Image Description" width="500"/>

```javascript

if(obnizParts.isFirstRepat !== true){
    return
}

obniz.switch.onchange = (pressed)=>{
    node.send({payload: pressed})
}

obnizParts.isFirstRepat = false;

```

また、obnizの初期化ノードに下記1行を追加してください。

```javascript

obnizParts.isFirstRepat = true;

```

5. 最後にtemplateノードを図のように設定し、テンプレートを貼り付けてください。
<img src="https://i.gyazo.com/f2b879e09dab01144ded904a0e1d3337.png" alt="Image Description" width="500"/>

テンプレート
```json
{ "text" : "{{payload}}"}
```

6. デプロイし、obnizのスイッチを右・左・真ん中に押し込み、Teamsに投稿されれば成功です！
<img src="https://i.gyazo.com/9c6ea27b073a3acdbf325a8a35c09dad.png" alt="Image Description" width="500"/>




#### 完成したフロー

※APIキー等は自分で入れてください

```JSON
[{"id":"12694ec6ee7fc64b","type":"inject","z":"cc81042a39216a8c","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"{\"text\": \"Node-REDから送信 \"}","payloadType":"json","x":330,"y":260,"wires":[["e3bab0936e7d3c87"]]},{"id":"e393ec67c7cbf180","type":"debug","z":"cc81042a39216a8c","name":"debug 14","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":760,"y":300,"wires":[]},{"id":"e3bab0936e7d3c87","type":"http request","z":"cc81042a39216a8c","name":"","method":"POST","ret":"obj","paytoqs":"ignore","url":"【Teams Webhook】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":570,"y":300,"wires":[["e393ec67c7cbf180"]]},{"id":"b9344fcaf32933ae","type":"template","z":"cc81042a39216a8c","name":"","field":"payload","fieldType":"msg","format":"json","syntax":"mustache","template":"{ \"text\" : \"{{payload}}\"}","output":"json","x":380,"y":360,"wires":[["e3bab0936e7d3c87","1678f485ee289c50"]]},{"id":"1678f485ee289c50","type":"debug","z":"cc81042a39216a8c","name":"debug 15","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":460,"y":480,"wires":[]},{"id":"f77c3a8f5ef3d55f","type":"obniz-repeat","z":"cc81042a39216a8c","obniz":"a5fae3ca0b96e551","name":"","interval":"3000","code":"if(obnizParts.isFirstRepat !== true){\n    return\n}\n\nobniz.switch.onchange = (pressed)=>{\n    node.send({payload: pressed})\n}\n\nobnizParts.isFirstRepat = false;\n","x":190,"y":360,"wires":[["b9344fcaf32933ae"]]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"obnizID","deviceType":"obnizboard1y","name":"","accessToken":"","code":"obniz.display.clear(); \nobniz.display.print('azure'); \nobnizParts.isFirstRepat = true;\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});\nobnizParts.hcsr04 = obniz.wired(\"HC-SR04\", { gnd: 8, echo: 9, trigger: 10, vcc: 11 });"}]

```




---


**[◀ 目次ページに戻る](./readme.md)**