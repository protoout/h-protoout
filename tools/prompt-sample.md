# プロンプトサンプル

## １. Node-REDのFunctionノードで使えるコードを生成

こちらのサンプルを変更しながら進めてみましょう。

```
## system

- 常にNode-REDのFunctionノードで利用できるコンテンツを返してください。
- 常にvarの代わりにconstかletを使います。
- 外部のノードモジュールを使用するように要求されない限り、require() を使用しないでください。
- 指示がない限り、基本的にコードとインラインコードコメントを返します。

## prompt
- センサーの値が送られてきます。センサーデータを元にセンサーの値が300以下かどうかで条件分岐して次のノードに渡す処理を書いて下さい。
- 条件分岐をして二つの出力先が作れるようにしてください。
```

>例: [ChatGPTの元画面](https://chat.openai.com/share/e/fc8b0125-7589-47a0-b9b8-45e1b9390186)

## 2. Node-REDでobnizノードが動くプロンプトサンプル

```
あなたはNode-REDとobnizを使ったIoTアプリケーション開発のエキスパートです。

以下の要件に基づいて、Node-REDのフローをJSONで生成してください。

要件:
- HC-SR04超音波距離センサーを使って距離を測定する
- 距離が200cm以下になったら、LEDを点灯する
- 距離が200cmより大きくなったら、LEDを消灯する
- obnizとNode-REDを使ってセンサーとLEDを制御する

フローの生成には、以下の点を厳密に守ってください。

1. obnizの設定ノード (型: "obniz")
   - プロパティ "code" 内で、以下の操作を行う
     - HC-SR04とLEDのピン設定を行い、`obnizParts` のプロパティとして追加する
       - HC-SR04: `obnizParts.hcsr04 = obniz.wired("HC-SR04", {gnd:0, echo:1, trigger:2, vcc:3});`
       - LED: `obnizParts.led = obniz.wired("LED", {anode:4, cathode:5});`
     - グローバル変数 `obnizParts` の初期化は不要

2. obniz repeatノード (型: "obniz-repeat")
   - プロパティ "interval" で、1秒ごとに実行するように設定する
   - プロパティ "code" 内で、以下のコードを厳密に記述する
     ```
     msg.payload = await obnizParts.hcsr04.measureWait(); //距離の測定
     return msg;
     ```
   - 他のノードにコードを記述しないこと

3. functionノード (型: "function")
   - プロパティ "func" 内で、以下の操作を行う
     - `msg.payload` の距離値を受け取り、しきい値（200cm）と比較する
     - しきい値以下ならば `msg.payload` に true、そうでない場合は false をセットして返す
   - obniz repeatノードとは別のノードとして作成すること

4. obniz functionノード (型: "obniz-function")
   - プロパティ "code" 内で、以下の操作を行う
     - `msg.payload` の真偽値を受け取り、LED を制御する
     - true ならば `obnizParts.led.on()`、false ならば `obnizParts.led.off()` を実行する

5. ノード間の接続と配置
   - obniz repeatノードの出力をfunctionノードに接続
   - functionノードの出力をobniz functionノードに接続
   - ノードは3つとし、横に並べて配置

6. 分かりやすい名前とコメントを各ノードに付ける

生成されたJSONは、マークダウン形式のコードブロックで出力してください。
```

## 3. Node-REDのフローを説明させる

フローを説明させるプロンプト例です。

```
以下はNode-REDのフローのJSONです。

このフローで行われている全ての処理内容を過不足無く、簡潔に説明してください。特に、obnizのスイッチやディスプレイの状態取得や制御、接続しているセンサーやアクチュエーターの制御、詳細に説明してください。

各処理がどのように連携しているかも含めて説明をお願いします。

```
[{"id":"5fa9057f.f2e0ac","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nreturn msg;","x":330,"y":340,"wires":[["ebafa559.00b978","e8f7976.0477568"]]},{"id":"ebafa559.00b978","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"obniz.display.clear(); // 画面を消去\r\n\r\nif (msg.payload === 'push') {\r\n // スイッチが押されている状態\r\n obniz.display.print('LED ON');\r\n obnizParts.led.on();\r\n} else {\r\n // スイッチが押されていない状態\r\n obniz.display.print('LED OFF');\r\n obnizParts.led.off();\r\n}\r\n","x":520,"y":340,"wires":[[]]},{"id":"e8f7976.0477568","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":510,"y":420,"wires":[]}]
```
```

## 4. 既存フローの回収

```
## 役割
あなたはNode-REDとobnizを使ったIoTアプリケーション開発のエキスパートです。

以下の要件に基づいて、Node-REDのフローをJSONで生成してください。

## 前提条件
- 常にNode-REDで利用できるコンテンツを返してください。
- コードを書く場合はFunctionノードで利用できるコードにしてください。常にvarの代わりにconstかletを使います。
- 外部のノードモジュールを使用するように要求されない限り、require() を使用しないでください。
- 指示がない限り、基本的にコードとインラインコードコメントを返します。
- functionノードを利用する際にobnizの処理が含まれる場合は常に、functionノードは使わずにobniz functionノードを利用してください。
- 各 `obniz-function` ノードは、次のノードに `msg` オブジェクトを渡すために `return msg;` を含むようにしてください。
- 入力にはNode-REDのフローとなるJSONと要件を渡します。

## 出力

- 出力スピードを上げるため、出力するフローのJSONはインデント無しでお願いします。
- 簡単な修正説明もお願いします。

## JSONと説明

```
[{"id":"5fa9057f.f2e0ac","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nreturn msg;","x":330,"y":340,"wires":[["ebafa559.00b978","e8f7976.0477568"]]},{"id":"ebafa559.00b978","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"obniz.display.clear(); // 画面を消去\r\n\r\nif (msg.payload === 'push') {\r\n // スイッチが押されている状態\r\n obniz.display.print('LED ON');\r\n obnizParts.led.on();\r\n} else {\r\n // スイッチが押されていない状態\r\n obniz.display.print('LED OFF');\r\n obnizParts.led.off();\r\n}\r\n","x":520,"y":340,"wires":[[]]},{"id":"e8f7976.0477568","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":510,"y":420,"wires":[]}]
```

obniz-repeat ノード: このノードは、obnizデバイスから定期的にスイッチの状態を取得します。interval パラメーターにより、取得の頻度が設定されています。

obniz-function ノード: このノードは、obnizデバイスから取得したスイッチの状態に基づいて、LEDの状態を制御します。msg.payload には、スイッチの状態が含まれます。スイッチが押されている場合は、LEDを点灯させ、画面に "LED ON" と表示します。スイッチが押されていない場合は、LEDを消灯させ、画面に "LED OFF" と表示します。

debug ノード: このノードは、デバッグ情報を表示します。この場合、obniz-function ノードからの出力が表示されます。

## 要件

- このフローはobniz functionノード内部に条件分岐コードが書いてあり、初学者には分かりにくいので、プログラム内で条件分岐コードは書かず必ずSwitchノードを使って切り替えるようなフローに書き換えてください。
- 現状のフローでは、LEDの処理とDisplayの処理が同じobniz functionノードに書かれているので機能ごとに細かく分解し、DisplayのON/OFFとLEDのON/OFFで4つのobniz functionノードを作ってください。
- Switchノードからの出力は、二つに条件分岐され、LEDとDisplayの処理がセットで実行されます。LED制御ノードの後ろにDisplay制御ノードを結線し、直列で実行してください。
- obnizのスイッチを監視する処理を行っているobniz repeatノードは変更を加えないでください。
- obniz repeatノードの後ろにはSwitchノードとdebugノードが結線され、その他は接続しないでください。
```