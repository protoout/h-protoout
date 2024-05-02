4. Keyestudio_TrafficLight（LED信号モジュール）

[Keyestudio_TrafficLightのパーツライブラリ](https://docs.obniz.com/ja/sdk/parts/Keyestudio_TrafficLight/README.md)

<img src="https://i.gyazo.com/a761dd9b2e6b058523ca062e14adb16d.jpg" alt="img" width= "500">

- obniz 0 - GND
- obniz 1 - G
- obniz 2 - Y
- obniz 3 - R

```JSON
[{"id":"871663456440f96f","type":"obniz-function","z":"922cab1da68a7d27","obniz":"a5fae3ca0b96e551","name":"","code":"obnizParts.light.single(msg.payload);\n\nreturn msg;","x":520,"y":640,"wires":[["d71cc6845528f6b3"]]},{"id":"daafa2b76adf4485","type":"inject","z":"922cab1da68a7d27","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"red","payloadType":"str","x":230,"y":560,"wires":[["871663456440f96f"]]},{"id":"08057ff0788ce9fd","type":"inject","z":"922cab1da68a7d27","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"green","payloadType":"str","x":230,"y":660,"wires":[["871663456440f96f"]]},{"id":"d71cc6845528f6b3","type":"debug","z":"922cab1da68a7d27","name":"debug 3","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":760,"y":640,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"","accessToken":"","code":"obniz.display.clear(); // 画面を消去\nobnizParts.light = obniz.wired(\"Keyestudio_TrafficLight\", { gnd: 0, green: 1, yellow: 2, red: 3 });"}]

```

▼初期化処理コード  
```javascript

obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:0, green:1, yellow:2, red:3});

```

#### 【Node-RED練習】黄色いランプを光らせてみよう！

Node-REDのフローを自分で変更して黄色いランプを光らせてみてください。




