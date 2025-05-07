# Teams API を連携して obniz Board から通知してみよう

みなさんが使っている Teams を Webhook という仕組みを使って Node-RED 経由で連携し、obniz Board で行った動作をトリガーとしてメッセージを送ってみます。

## Webhook とは？

特定のイベントが発生したこと（Teams にメッセージが投稿されたなど）をトリガーとして別のアプリケーションにリアルタイムな情報提供を行う仕組みです。

少し、どういうことか捉えやすいように具体例をあげてみます。

### 1. Webhook に対応しているサービス

具体的に、Webhook が利用できるサービスはどんなものがあるか見てみましょう。

- Teams
- Slack
- Discord
- PayPay
- PayPal
- LINE
...

Webhook を使うことで、

- 決済システムの取引が行われたときに LINE へ通知する

- お問い合わせメールが来たときに Teams へ通知する

このようなこともできるでしょう。

<br><br>

うまく使えば、チーム間のコミュニケーション促進や、業務効率にも役立ちます！

ではさっそく、チャレンジしてみましょう。


## 完成イメージ

obniz Board のスイッチを押して、Teams に投稿するものを作ります。

<img width="450" alt="image" src="https://github.com/user-attachments/assets/eddea5a2-c085-45f7-9d55-25bbb38baba7" />  

右のスイッチを押すと"right"と通知されます。    
<img width="450" alt="image" src="https://github.com/user-attachments/assets/b235a549-e01b-4b8c-a972-2fd5c1bb26c3" />




## やってみよう

### 1. Teams に Node-RED からメッセージを送ってみる

1. `injectノード`、`http requestノード`、`debugノード`を追加し図のようにつなぐ

<a href="https://gyazo.com/7d06640b02dbe05463a58a88481a182d"><img src="https://i.gyazo.com/7d06640b02dbe05463a58a88481a182d.png" alt="Image from Gyazo" width="450"/></a>

2. `http request`ノードを図のように設定する。

URLには[こちら]()の Teams webhook の URL を入力してください。

> [!CAUTION]
> ランスルーではこちらをつかいます
> `https://prod-42.japaneast.logic.azure.com/workflows/b9f93af31f86427eab8c7271753d4b77/triggers/manual/paths/invoke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=PhJpR2q-tXRG7AntX_hex1p5yIkS9iQ1o85E6zUIBsk`

<img src="https://i.gyazo.com/6e48aee0cabc082df0fe1242df9e878f.png" alt="Image from Gyazo" width="450"/>

■ メソッドについて

- `http requestノード`はサーバーに対し「これやって」（今回はメッセージの送信）と、リクエストをするために使います。

[HTTPについてはこちら](/tools/column/iot-overview/03-network.md)

HTTPリクエスト（サーバーへの要求方法）にはいくつかの種類があります。

- GET: 情報をもらう
- POST: 情報を投稿する

ほかにも、PUT/DELETEなどがあり、用途によって使い分けします。

今回は Teams にメッセージを送信するため、**POST** を使います。
  

3. `templateノード`を使って送信するメッセージを作る

まずは、任意のメッセージを Teams に送れるようにしましょう。


`templateノード`を追加し、以下のように設定します。

<a href="https://gyazo.com/57f6790f1191a08acb601ca2e99dfa5d"><img src="https://i.gyazo.com/57f6790f1191a08acb601ca2e99dfa5d.gif" alt="Image from Gyazo" width="500"/></a>

なお、出力形式は`JSON`にします。  
![image](https://github.com/user-attachments/assets/729a5d41-089f-4a94-b9b2-ed647ed1fa43)


中には、テンプレートの中身を書き換えて記入してください。

テンプレート
```json
{
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "TextBlock",
            "text": "【好きな食べ物の名前に書き換えてください】",
            "wrap": true,
            "markdown": true
          }
        ]
      }
    }
  ]
}
```

このテンプレートの書き方は、各サービスプロバイダー（今回はMS）が Webhook の仕様をどのようにしているか？によってかわります。


4. 試してみよう

デプロイして、`injectノード`のボタンをクリックしてみてください。

Teams に送信されれば成功です！

<a href="https://gyazo.com/1c147c03b3952b1fa33621380d3a7117"><img src="https://i.gyazo.com/1c147c03b3952b1fa33621380d3a7117.png" alt="Image from Gyazo" width="400"/></a>


### 2. obniz Board からメッセージを送るようにする

では次に、obniz Board からメッセージを送る部分を作ります

1. obniz Board のスイッチの状態を取得する
スイッチの[マニュアル](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-obniz-switch)を参考に、スイッチの状態が出るところまで行ってください。

3. `switchノード`を配置し、設定する

obniz Board のスイッチの状態によって、left, right, pushの3種類のメッセージを出し分けるようにします。

<a href="https://gyazo.com/152ac92d21b3e2b7da854d2f04dadbc4"><img src="https://i.gyazo.com/152ac92d21b3e2b7da854d2f04dadbc4.gif" alt="Image from Gyazo" width="600"/></a>


`switchノード`から`templateノード`につないでください。

<a href="https://gyazo.com/af8397913d2d0f01a8f8c6a80f518b41"><img src="https://i.gyazo.com/af8397913d2d0f01a8f8c6a80f518b41.gif" alt="Image from Gyazo" width="600"/></a>


3. 最後に`templateノード`の中身を書き換えてください。
<img src="https://i.gyazo.com/f2b879e09dab01144ded904a0e1d3337.png" alt="Image Description" width="500"/>

テンプレート
```json
{
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "TextBlock",
            "text": "{{payload}}を押したよ",
            "wrap": true,
            "markdown": true
          }
        ]
      }
    }
  ]
}

```

6. デプロイし、obniz Board のスイッチを右・左・真ん中に押し込み、Teams  に投稿されれば成功です！
<img src="https://i.gyazo.com/9c6ea27b073a3acdbf325a8a35c09dad.png" alt="Image Description" width="500"/>



#### 完成したフロー

```JSON
[{"id":"9270543960c8af4d","type":"inject","z":"e6348621e7068ade","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":280,"y":500,"wires":[["1596b3bce49c2509"]]},{"id":"40bd6e702c6030b5","type":"debug","z":"e6348621e7068ade","name":"debug 29","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":820,"y":500,"wires":[]},{"id":"88ad3ce521e597ba","type":"http request","z":"e6348621e7068ade","name":"","method":"POST","ret":"obj","paytoqs":"ignore","url":"","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":630,"y":500,"wires":[["40bd6e702c6030b5"]]},{"id":"1596b3bce49c2509","type":"template","z":"e6348621e7068ade","name":"","field":"payload","fieldType":"msg","format":"json","syntax":"mustache","template":"{\n    \"text\": \"{{payload}}を押したよ\"\n}","output":"str","x":460,"y":500,"wires":[["88ad3ce521e597ba"]]},{"id":"977e7e827c1878bc","type":"obniz-repeat","z":"e6348621e7068ade","obniz":"a5fae3ca0b96e551","name":"","interval":100,"code":"msg.payload = await obniz.switch.getWait(); //msg.payloadにobnizのスイッチの状態を格納\n\nreturn msg; //msg.payloadを出力","x":150,"y":320,"wires":[["cdafc18892dab7bf","a398a0eaa8fadb75"]]},{"id":"cdafc18892dab7bf","type":"debug","z":"e6348621e7068ade","name":"debug 30","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":560,"y":320,"wires":[]},{"id":"a398a0eaa8fadb75","type":"switch","z":"e6348621e7068ade","name":"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"right","vt":"str"},{"t":"eq","v":"left","vt":"str"},{"t":"eq","v":"push","vt":"str"}],"checkall":"true","repair":false,"outputs":3,"x":350,"y":380,"wires":[["1596b3bce49c2509"],["1596b3bce49c2509"],["1596b3bce49c2509"]]},{"id":"f69530ebd58957df","type":"comment","z":"e6348621e7068ade","name":"obnizのスイッチを押すとteamsにメッセージを送る","info":"","x":270,"y":260,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"","deviceType":"obnizboard1y","name":"","accessToken":"","code":" "}]

```

※ API キーが違うのでこのままでは使えません。あくまで例としてご理解ください。

## 応用： 他のセンサーと組み合わせて使ってみよう


- [熱中症アラートをつくろう](/tools/tutorials/01_temp_led.md)と組み合わせて、暑さ指数のレベルを Teams に通知して、みんなの熱中症を予防する
- [照度センサー(CdS)](/tools/parts-manual/sensor/cds.md)を自分のおやつの下に置いておき、誰かが取ったら Teams に通知するおやつ監視システム

などなど...
Teams への通知だけでも、プライベート・業務で色々なことができます。

---


**[◀ 目次ページに戻る]( ../readme.md)**
