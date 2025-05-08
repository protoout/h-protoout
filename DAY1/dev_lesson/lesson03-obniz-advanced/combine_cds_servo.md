# 明るさによってサーボーモーターの動きを変えよう

> <a href="https://gyazo.com/fc47d3de9f7c1f81247fefdf3d041de5"><img src="https://i.gyazo.com/fc47d3de9f7c1f81247fefdf3d041de5.png" alt="Image from Gyazo" width="450"/></a>
>    
> ソーラーパネルは効率的に太陽光エネルギーを回収するために照度に合わせてパネルの角度を変える仕組みになっていると言われています。
> その他にも、スマートブラインド[^5]などにも同様の仕組みが使われています。

## 完成イメージ

明るいとサーボモーターが90度、暗いと0度になります。　

<a href="https://gyazo.com/644d6b8e52829099c1bd30a7a21e1db1"><img src="https://i.gyazo.com/644d6b8e52829099c1bd30a7a21e1db1.gif" alt="Image from Gyazo" width="450"/></a>

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
[{"id":"74370c53acbdd5c8","type":"obniz-repeat","z":"33fef8602cdc39ab","obniz":"","name":"","interval":100,"code":"const voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得\r\n\r\nmsg.payload = voltage;\r\n\r\nreturn msg;","x":290,"y":1280,"wires":[["fe5977dfc7869d6e"]]},{"id":"fe5977dfc7869d6e","type":"debug","z":"33fef8602cdc39ab","name":"debug 7","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":520,"y":1280,"wires":[]},{"id":"891f0f18676e8edc","type":"comment","z":"33fef8602cdc39ab","name":"Cds","info":"","x":170,"y":1240,"wires":[]},{"id":"8097414a64e90d4d","type":"comment","z":"33fef8602cdc39ab","name":"obniz ID と device type をご自身のものに書き換えてください！","info":"","x":350,"y":1320,"wires":[]}]
```
  
- サーボモーターのJSON
```JSON
[{"id":"a1208aa62d74848a","type":"inject","z":"33fef8602cdc39ab","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":300,"y":1460,"wires":[["7a90862abd46e20b"]]},{"id":"dd7c33f85b23e2e0","type":"comment","z":"33fef8602cdc39ab","name":"サーボモーター","info":"","x":200,"y":1420,"wires":[]},{"id":"7a90862abd46e20b","type":"change","z":"33fef8602cdc39ab","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"20","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":440,"y":1520,"wires":[["529f81519673ba8a"]]},{"id":"529f81519673ba8a","type":"obniz-function","z":"33fef8602cdc39ab","obniz":"","name":"","code":"obnizParts.servo.angle(msg.payload); //msg.payloadの角度にサーボモーターを動かす\r\n\r\nreturn msg //msgを出力","x":580,"y":1580,"wires":[["d01c753befd17a54"]]},{"id":"d01c753befd17a54","type":"debug","z":"33fef8602cdc39ab","name":"debug 8","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":720,"y":1620,"wires":[]},{"id":"0456e3e8973f29bc","type":"comment","z":"33fef8602cdc39ab","name":"obniz ID と device type をご自身のものに書き換えてください！","info":"","x":350,"y":1660,"wires":[]}]
```

> [!WARNING]
> obniz ID と device type はご自身のものに書きかえる必要があります。
  
## 動作を試す
ここまでできたらデプロイし、明るさの違いによってサーボモーターの角度が変われば成功です！

---

**[◀ 目次ページに戻る](../readme.md)**
