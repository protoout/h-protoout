# 距離に応じてライトの色を変えてみよう

### 感知式信号機  
車があまり通らない場所では、車がいることを超音波センサで感知してから信号機のライトを制御する仕組みになっています。    
停止線より手前で止まりすぎると信号が変わらないということも...  

<img width="400" alt="image" src="https://github.com/user-attachments/assets/36f6f62e-ea25-4130-98ed-38a856dce850" />  

### このような仕組みを Node-RED 作ってみましょう  
超音波センサの検知する物体が一定の距離以上近づくと、ライトの色が変わる、という仕組みです。  

```mermaid

graph TD;
    A[パトランプは赤] --> B[物体が超音波センサに近づく];
    B --> C{距離が150mm以下};
    C --> |Yes| D[3秒後にパトランプは青（緑）];
    D --> E[5秒後にパトランプは黄];
    C --> |No| E\F[何も起きない];

```

### 1. obniz Board での配線

#### インジケーター: パトランプ  
> [!WARNING]
> **極性(+ -)があるため、接続に間違いがないか注意**

![image](https://github.com/user-attachments/assets/16f15ee7-74ef-48d8-944a-31f4370f16c2)

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  | obnizの3番    |
| G  | obnizの4番    |
| Y  | obnizの5番    |
| R  | obnizの6番    |

#### センサー: 超音波距離センサー

![image](https://github.com/user-attachments/assets/706b3ed4-6e23-4e44-9739-20b27c0c2282)

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  | obnizの8番    |
| Edho  | obnizの9番    |
| Trig  | obnizの10番    |
| Vcc  | obnizの11番    |

> [!NOTE]
> obniz Board がごちゃごちゃしてきてますが問題ありません
>   
> ※パトランプゲットしたら画像入れる
  
### 2. 使うノードとつなぎ方
    
- `obniz repeatノード`
- `switchノード`
- `obniz-functionノード`
- `debugノード`

![image](https://github.com/user-attachments/assets/6c80c2bc-79bc-4b0b-a322-cbce5a2dc3f4)
  

### 3. 初期化処理コードの編集
  
```js
obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:3, green:4, yellow:5, red:6});
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:8, echo:9, trigger:10, vcc:11 }); //8,9,10,11番にピンを割り当てる
```
  
### 4. 各ノードの設定方法

- `obniz repeatノード`のコード

```js
msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力
```

- `switchノード`
  
>  payload が150mm より小さいか150mm以上か、という条件をつくります。  
> ![image](https://github.com/user-attachments/assets/58a9ab04-8e11-449c-9350-079a80fdb399)
  
> データの型を数値にするのをお忘れなく！  
> ![image](https://github.com/user-attachments/assets/70a537b1-dfff-4569-8b9e-1f23595b20f4)

  
- `changeノード`   
payloadが150mmより小さければ `green` という値を渡すようにします。  
![image](https://github.com/user-attachments/assets/67d610ca-e5d6-47ad-bc3f-e08cc7c3a35d)

同様に、150mm以上なら `red` にします。   
この色の文字列をパトランプが受け取ることで色を変えることができます。  

- Green の `obniz-functionノード`のコード

```js
obniz.wait(3000);
obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる
obniz.wait(5000);
light.single("yellow");

return msg;
```

- Red の `obniz-functionノード`のコード

```js
obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる

return msg;
```


### 5. 結果

距離が近づいた時にLEDの色が変われば OK です！

> [!CAUTION]
> **`obniz-close` で停止するのをお忘れなく！**


### 6. そろそろノードが複雑に...  

電子部品を組み合わせると obniz ノードだけでなく条件分岐などもあってノードが複雑になってきます。
実は、このノードを簡単に出し入れすることができます。

> ノードの塊を左クリックで囲んで指定します。指定するとオレンジ色の枠が出ます。
> <img width="500" alt="image" src="https://github.com/user-attachments/assets/d5bd307c-1204-483f-9fbc-0e75e20203ba" />

> この状態で右側のハンバーガーメニューから`書き出し`を選びます。
> <img width="500" alt="image" src="https://github.com/user-attachments/assets/29aae6ed-69aa-4712-9a9d-5970753da2bb" />

> `選択したフロー`、`インデントなし`、`JSON`を選んで`書き出し`を押すと先ほどのフローがコピーされた状態になります。
> <img width="500" alt="image" src="https://github.com/user-attachments/assets/8d501c79-ba34-44dc-908c-0d66e17cf753" />

中味はこのようなものです。JSON という形式で先ほどのノードが示されています。
```JSON
[{"id":"d82216061e268340","type":"comment","z":"fcf566e83f304c66","name":"感知式信号機","info":"","x":110,"y":740,"wires":[]},{"id":"33c441a240ac24bf","type":"obniz-repeat","z":"fcf566e83f304c66","obniz":"3a214050aa255b4f","name":"","interval":100,"code":"msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納\r\n\r\nreturn msg; //msg.payloadを出力","x":110,"y":800,"wires":[["0475abc22f78c73a"]]},{"id":"0475abc22f78c73a","type":"switch","z":"fcf566e83f304c66","name":"","property":"payload","propertyType":"msg","rules":[{"t":"lt","v":"150","vt":"num"},{"t":"gte","v":"150","vt":"num"}],"checkall":"true","repair":false,"outputs":2,"x":210,"y":860,"wires":[["d868b775d6aebf01"],["d8f182c07e576548"]]},{"id":"076fd1f5459975fe","type":"obniz-function","z":"fcf566e83f304c66","obniz":"3a214050aa255b4f","name":"","code":"\r\nobniz.wait(3000);\r\nobnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる\r\nobniz.wait(5000);\r\nlight.single(\"yellow\");\r\n\r\nreturn msg;\r\n","x":560,"y":820,"wires":[["903c0a52d558bfbc"]]},{"id":"903c0a52d558bfbc","type":"debug","z":"fcf566e83f304c66","name":"debug 2","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":740,"y":860,"wires":[]},{"id":"d868b775d6aebf01","type":"change","z":"fcf566e83f304c66","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"green","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":820,"wires":[["076fd1f5459975fe"]]},{"id":"d8f182c07e576548","type":"change","z":"fcf566e83f304c66","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"red","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":380,"y":900,"wires":[["d2b1634250baba16"]]},{"id":"d2b1634250baba16","type":"obniz-function","z":"fcf566e83f304c66","obniz":"3a214050aa255b4f","name":"","code":"obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる\r\n\r\nreturn msg;","x":560,"y":900,"wires":[["903c0a52d558bfbc"]]},{"id":"3a214050aa255b4f","type":"obniz","obnizId":"82630676","deviceType":"obnizboard1y","name":"","accessToken":"","autoConnectOnDeploy":true,"code":"obnizParts.light = obniz.wired(\"Keyestudio_TrafficLight\", {gnd:3, green:4, yellow:5, red:6});\r\nobnizParts.hcsr04 = obniz.wired(\"HC-SR04\",{ gnd:8, echo:9, trigger:10, vcc:11 }); //8,9,10,11番にピンを割り当てる"}]
```

では今度は、同じハンバーガーメニューから`読み込み`を選択し、先ほどコピーされた JSON データを貼り付けます。
![image](https://github.com/user-attachments/assets/83736168-21ec-48df-8896-a09ef8fafd50)

>  `読み込み`を押すと先ほどと同じノードが出現します。(ポップアップが出るので`コピーを読み込み`を選びます)
> ![image](https://github.com/user-attachments/assets/57fe3c9e-26c0-423a-a389-cc6f0d664be2)

##### さて、この JSON 形式のデータを使えると何が嬉しいでしょうか？
  
> [!IMPORTANT]
> そう、生成 AI のプロンプトに入れることができるんですね！！
> この部分は Day2 で触れていくのでお楽しみに！
  
----  
  
[◀ Lesson1に戻る](../)
