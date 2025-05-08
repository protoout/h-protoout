# 明るさによってサーボーモーターの動きを変えよう

> <a href="https://gyazo.com/fc47d3de9f7c1f81247fefdf3d041de5"><img src="https://i.gyazo.com/fc47d3de9f7c1f81247fefdf3d041de5.png" alt="Image from Gyazo" width="450/></a>
>    
> ソーラーパネルは効率的に太陽光エネルギーを回収するために照度に合わせてパネルの角度を変える仕組みになっていると言われています。
> その他にも、スマートブラインド[^5]などにも同様の仕組みが使われています。

## 完成イメージ

明るいとサーボモーターが90度、暗いと0度になります。

<a href="https://gyazo.com/371d98adc6a3a8e67e192c4132de5cd2"><img src="https://i.gyazo.com/371d98adc6a3a8e67e192c4132de5cd2.gif" alt="Image from Gyazo" width="472"/></a>

## つくってみよう
こちらのマニュアルを参考に実装してみましょう。ブレッドボードを使うので、資料を見ながら配線の仕方を真似してください。  
  
#### ■[チュートリアル: サーボとCdS連動システム](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/tutorial-servo-cds)  

ブレッドボードの使いかたは[こちら](https://dotstud.io/docs/breadboard/)を参考にしてください。  

### 余裕があれば試してみよう  
上記のマニュアルで使用するフローの JSON をこちらに用意しました。これでノードを一つ一つ設定する手間を省くことができます。
以下の JSON を読み込んで資料と照らし合わせながら実装を進めてみてください。    
JSON の書き出しについては[前の演習ページ](../lesson03-obniz-advanced/combine_trafficlight_ultrasound.md)を参考にしましょう。

- CdsのJSON
```JSON
[{"id":"e900f9ef901919b3","type":"obniz-repeat","z":"33fef8602cdc39ab","obniz":"ba70d68aaeef2385","name":"","interval":100,"code":"const voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得\r\n\r\nmsg.payload = voltage;\r\n\r\nreturn msg;","x":930,"y":80,"wires":[["1f1a09fd1795cc78"]]},{"id":"1f1a09fd1795cc78","type":"debug","z":"33fef8602cdc39ab","name":"debug 7","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":1160,"y":80,"wires":[]},{"id":"a44a779093b2a813","type":"comment","z":"33fef8602cdc39ab","name":"Cds","info":"","x":810,"y":40,"wires":[]},{"id":"b336febe1bc5770c","type":"comment","z":"33fef8602cdc39ab","name":"obniz ID と device type をご自身のものに書き換えてください！","info":"","x":990,"y":120,"wires":[]},{"id":"ba70d68aaeef2385","type":"obniz","obnizId":"11111111","deviceType":"obnizboard1y","name":"","accessToken":"","autoConnectOnDeploy":true,"code":"obniz.io0.output(true); //io0番を5vに\r\nobniz.io2.output(false); //io2番をGNDに\r\nobnizParts.servo = obniz.wired(\"ServoMotor\",{ signal:2 }); //サーボモーターをどのくらい回すかの信号を2番に設定"}]
```
  
- サーボモーターのJSON
```JSON
[{"id":"eceaced9cf2dbae7","type":"inject","z":"33fef8602cdc39ab","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":940,"y":220,"wires":[["75ebdb6040cf49df"]]},{"id":"dce4052f4e01d17c","type":"comment","z":"33fef8602cdc39ab","name":"サーボモーター","info":"","x":840,"y":180,"wires":[]},{"id":"75ebdb6040cf49df","type":"change","z":"33fef8602cdc39ab","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"20","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":1080,"y":280,"wires":[["9f0512b7835f523f"]]},{"id":"9f0512b7835f523f","type":"obniz-function","z":"33fef8602cdc39ab","obniz":"ba70d68aaeef2385","name":"","code":"obnizParts.servo.angle(msg.payload); //msg.payloadの角度にサーボモーターを動かす\r\n\r\nreturn msg //msgを出力","x":1220,"y":340,"wires":[["832e0df02cc239df"]]},{"id":"832e0df02cc239df","type":"debug","z":"33fef8602cdc39ab","name":"debug 8","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":1360,"y":380,"wires":[]},{"id":"b6cb1ebdf22a2df6","type":"comment","z":"33fef8602cdc39ab","name":"obniz ID と device type をご自身のものに書き換えてください！","info":"","x":990,"y":420,"wires":[]},{"id":"ba70d68aaeef2385","type":"obniz","obnizId":"11111111","deviceType":"obnizboard1y","name":"","accessToken":"","autoConnectOnDeploy":true,"code":"obniz.io0.output(true); //io0番を5vに\r\nobniz.io2.output(false); //io2番をGNDに\r\nobnizParts.servo = obniz.wired(\"ServoMotor\",{ signal:2 }); //サーボモーターをどのくらい回すかの信号を2番に設定"}]
```

> [!WARNING]
> obniz ID と device type はご自身のものに書きかえる必要があります。
  
## 動作を試す
ここまでできたらデプロイし、明るさの違いによってサーボモーターの角度が変われば成功です！

---

**[◀ 目次ページに戻る](../readme.md)**
