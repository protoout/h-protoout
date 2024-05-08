# Keyestudio_TrafficLight（LED信号モジュール）

### **新しいことをはじめる前に**  

[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。


---

## やってみよう

[Keyestudio_TrafficLightのパーツライブラリ](https://docs.obniz.com/ja/sdk/parts/Keyestudio_TrafficLight/README.md)


1. obnizにLED信号モジュールを接続する
<img src="https://i.gyazo.com/a761dd9b2e6b058523ca062e14adb16d.jpg" alt="img" width= "500">

- obniz 0 - GND
- obniz 1 - G
- obniz 2 - Y
- obniz 3 - R

2. Node-REDに下記フローを読み込む

```JSON
[{"id":"e596da97fcc3347f","type":"inject","z":"9e8495df15f468a7","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"red","payloadType":"str","x":170,"y":200,"wires":[["84b22ff78427aabe"]]},{"id":"a4d4f9837d757ce0","type":"inject","z":"9e8495df15f468a7","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"green","payloadType":"str","x":170,"y":300,"wires":[["84b22ff78427aabe"]]},{"id":"37213fb490f6b9cb","type":"debug","z":"9e8495df15f468a7","name":"debug 3","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":700,"y":280,"wires":[]},{"id":"84b22ff78427aabe","type":"obniz-function","z":"9e8495df15f468a7","obniz":"","name":"","code":"obnizParts.light.single(msg.payload);\n\nreturn msg;","x":460,"y":280,"wires":[["37213fb490f6b9cb"]]}]

```

3. 初期化処理のコードを書き換える

▼初期化処理コード

```javascript

obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:0, green:1, yellow:2, red:3});

```

## 2.演習

### 2-1. 黄色いランプを光らせてみよう！

Node-REDのフローを自分で変更して黄色いランプを光らせてみてください。


### 2-2. 【応用】温度センサーの値に応じてライトの色が変わるようにしよう

| 温度 | 色 |
|----------|----------|
| 30℃以上   | 赤  |
| 25℃以上30未満   | 黄色  |
| 24℃未満  | 緑 |



---

**[◀ 目次ページに戻る](../readme.md)**