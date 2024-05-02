# ダッシュボードにデータの表示・操作を行おう

## 目標
GUI（画面で操作できるユーザーインタフェース）にセンサーの値を表示したり、操作したりできるようになる。

## やってみよう

### 完成イメージ

node-red-dashboardを使い、GUI（画面で操作できるユーザーインタフェース）を作ってみましょう。


### 完成したフロー

```JSON

[{"id":"35131428dc29ef13","type":"tab","label":"lesson4-1","disabled":false,"info":"","env":[]},{"id":"dda95691c8ab3ced","type":"debug","z":"35131428dc29ef13","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":590,"y":140,"wires":[]},{"id":"eae6eb14b4f274ea","type":"obniz-function","z":"35131428dc29ef13","obniz":"a5fae3ca0b96e551","name":"","code":"msg.payload = \"finish\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":420,"y":140,"wires":[["dda95691c8ab3ced"]]},{"id":"b12a3a54eac0d2b3","type":"inject","z":"35131428dc29ef13","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":240,"y":140,"wires":[["eae6eb14b4f274ea"]]},{"id":"e42d3d96.12046","type":"obniz-repeat","z":"35131428dc29ef13","obniz":"a5fae3ca0b96e551","name":"","interval":"1000","code":"msg.payload = await obnizParts.hcsr04.measureWait();\n\nobniz.display.clear(); // クリア\nobniz.display.print('Ready');\n\n// 距離を取得\nlet distance = msg.payload;\n// そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい\ndistance = Math.floor(distance);\n\n// 距離(mm)をデバッグに表示\nmsg.payload = (distance + ' mm');\n// obnizディスプレイに表示\n// 一度消してから距離+mmの単位を表示\nobniz.display.clear();\nobniz.display.print(distance + ' mm');\n\n// 距離がある程度未満かどうかの判定\nif (distance < 50) { // 50mm = 5cm 以下の場合\n    // obnizディスプレイに近接していることを表示\n    obniz.display.clear();\n    obniz.display.print('Too close!!');\n}\n\nreturn msg;","x":210,"y":260,"wires":[["402408dd.31b188","0ca654b2a0720711"]]},{"id":"402408dd.31b188","type":"debug","z":"35131428dc29ef13","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":450,"y":260,"wires":[]},{"id":"0ca654b2a0720711","type":"ui_gauge","z":"35131428dc29ef13","name":"","group":"4a03c246.55f3d8","order":0,"width":0,"height":0,"gtype":"gage","title":"距離センサーの値","label":"units","format":"{{value}}","min":0,"max":"1000","colors":["#00b500","#e6e600","#ca3838"],"seg1":"","seg2":"","diff":false,"className":"","x":510,"y":340,"wires":[]},{"id":"1a04d0afa2a334fa","type":"ui_button","z":"35131428dc29ef13","name":"","group":"4a03c246.55f3d8","order":1,"width":"2","height":"2","passthru":false,"label":"ON","tooltip":"","color":"","bgcolor":"","className":"","icon":"","payload":"true","payloadType":"bool","topic":"topic","topicType":"msg","x":190,"y":440,"wires":[["7d924bb87f65f00c"]]},{"id":"7d924bb87f65f00c","type":"obniz-function","z":"35131428dc29ef13","obniz":"a5fae3ca0b96e551","name":"","code":"\nif(msg.payload == true){\n    obnizParts.led.on();\n}else{\n    obnizParts.led.off();\n}","x":420,"y":480,"wires":[["a5263b3e55071bef"]]},{"id":"58738820ac42baee","type":"ui_button","z":"35131428dc29ef13","name":"","group":"4a03c246.55f3d8","order":1,"width":"2","height":"2","passthru":false,"label":"OFF","tooltip":"","color":"","bgcolor":"","className":"","icon":"","payload":"false","payloadType":"bool","topic":"topic","topicType":"msg","x":190,"y":540,"wires":[["7d924bb87f65f00c"]]},{"id":"a5263b3e55071bef","type":"debug","z":"35131428dc29ef13","name":"debug 9","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":620,"y":480,"wires":[]},{"id":"a5fae3ca0b96e551","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"キサイチobniz","accessToken":"","code":"obniz.display.clear(); // 画面を消去\nobnizParts.led = obniz.wired(\"LED\", {anode:0, cathode:1});\nobnizParts.hcsr04 = obniz.wired(\"HC-SR04\", { gnd: 8, echo: 9, trigger: 10, vcc: 11 });"},{"id":"4a03c246.55f3d8","type":"ui_group","name":"Default","tab":"ccec3682.947098","order":1,"disp":true,"width":"6","collapse":false},{"id":"ccec3682.947098","type":"ui_tab","name":"Home","icon":"dashboard","order":1}]

```


---

## まとめ

基本的な操作ができるようになり、Node-RED上でObnizを操作できるようになりました！

次は...もっと色々なセンサーを触って、アイデアを広げていきましょう！
