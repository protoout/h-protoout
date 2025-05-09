# 距離に応じてライトの色を変えてみよう

##  debugノードの説明をします。
debug ノードでは出力去れた値を表示することができます。
      
![image](https://github.com/user-attachments/assets/06938ffe-3c0d-4818-984e-c36018a18e5a)  
  
画面では超音波距離センサで取得した値を見ることができます。     
<img width="431" alt="image" src="https://github.com/user-attachments/assets/d42e1719-8dc8-4fb3-873d-c9e3bee674df" />
  

### 感知式信号機  
車があまり通らない場所では、車がいることを超音波センサで感知してから信号機のライトを制御する仕組みになっています。    
停止線より手前で止まりすぎると信号が変わらないということも...  

<a href="https://gyazo.com/7b28a36cc8e2d80057c13f8609a4d158"><img src="https://i.gyazo.com/7b28a36cc8e2d80057c13f8609a4d158.png" alt="Image from Gyazo" width="450"/></a>


### このような仕組みを Node-RED 作ってみましょう  
超音波センサの検知する物体が一定の距離以上近づくと、ライトの色が変わる、という仕組みです。  

<details>

<summary>フローで書くとこんな感じです</summary>

```mermaid

graph TD;
    A[パトランプは赤] --> B[物体が超音波センサに近づく];
    B --> C{距離が150mm以下};
    C --> |Yes| D[3秒後にパトランプは青（緑）];
    D --> E[5秒後にパトランプは黄];
    C --> |No| E\F[何も起きない];

```

</details>

### 1. obniz Board での配線

#### インジケーター: パトランプ  
  
> [!WARNING]
> **極性(+ -)があるため、接続に間違いがないか注意**
  
<a href="https://gyazo.com/9a715ad65c4dc1cfae640c877bc7c0da"><img src="https://i.gyazo.com/9a715ad65c4dc1cfae640c877bc7c0da.png" alt="Image from Gyazo" width="450"/></a>


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  | obnizの3番    |
| G  | obnizの4番    |
| Y  | obnizの5番    |
| R  | obnizの6番    |

#### センサー: 超音波距離センサー

<a href="https://gyazo.com/640b3e50d2f9b454699893f110a7dcf0"><img src="https://i.gyazo.com/640b3e50d2f9b454699893f110a7dcf0.png" alt="Image from Gyazo" width="450"/></a>


| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  | obnizの8番    |
| Echo  | obnizの9番    |
| Trig  | obnizの10番    |
| Vcc  | obnizの11番    |

> [!NOTE]
> obniz Board がごちゃごちゃしてきてますが問題ありません
>
> <a href="https://gyazo.com/5672d9890a9177d0e5b8513be580f9d3"><img src="https://i.gyazo.com/5672d9890a9177d0e5b8513be580f9d3.jpg" alt="Image from Gyazo" width="450"/></a>

  
### 2. 使うノードとつなぎ方
    
- `obniz repeatノード`
- `switchノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`

<a href="https://gyazo.com/c6940412d192bb105795423023426451"><img src="https://i.gyazo.com/c6940412d192bb105795423023426451.png" alt="Image from Gyazo" width="600"/></a>

  

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
  
payload が150mm より小さいか150mm以上か、という条件をつくります。  
  
> <a href="https://gyazo.com/02c7f39d3fc3cb42140fa2f6f7ad548a"><img src="https://i.gyazo.com/02c7f39d3fc3cb42140fa2f6f7ad548a.png" alt="Image from Gyazo" width="450"/></a>
    
> <a href="https://gyazo.com/c10f54cad5d86054c0dca296bad97b8d"><img src="https://i.gyazo.com/c10f54cad5d86054c0dca296bad97b8d.png" alt="Image from Gyazo" width="450"/></a>

>   
> データの型を数値にするのをお忘れなく！

  
- `changeノード`   
payloadが150mmより小さければ `green` という値を渡すようにします。

<a href="https://gyazo.com/9a2ed1386565942c7b7907d73bf3ac39"><img src="https://i.gyazo.com/9a2ed1386565942c7b7907d73bf3ac39.png" alt="Image from Gyazo" width="450"/></a>

同様に、150mm以上なら `red` にします。   
この色の文字列をパトランプが受け取ることで色を変えることができます。  

- Green の `obniz-functionノード`のコード

```js
obniz.wait(3000);
obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる
obniz.wait(5000);
obnizParts.light.single("yellow");

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


### 6. そろそろフローが複雑に...  

電子部品を組み合わせると obniz ノードだけでなく条件分岐などもあってフローが複雑になってきます。
実は、このノードを簡単に出し入れすることができます！
  
ノードの塊を左クリックで囲んで指定します。指定するとオレンジ色の枠が出ます。  
<a href="https://gyazo.com/248b39613afc0bed77583f2095976596"><img src="https://i.gyazo.com/248b39613afc0bed77583f2095976596.png" alt="Image from Gyazo" width="450"/></a>
  
この状態で右側のハンバーガーメニューから`書き出し`を選びます。  
<a href="https://gyazo.com/af2d28f69284105f70d514d9502bed87"><img src="https://i.gyazo.com/af2d28f69284105f70d514d9502bed87.png" alt="Image from Gyazo" width="450"/></a>
  
`選択したフロー`、`インデントなし`、`JSON`を選んで``ダウンロード`を選ぶと、JSON ファイルを PC 上(ローカル) に保存できます。 なお、`書き出し`を押すと先ほどのフローがコピーされた状態になります。  
<a href="https://gyazo.com/022423398cb7fc25cb2bdbcd0f259499"><img src="https://i.gyazo.com/022423398cb7fc25cb2bdbcd0f259499.png" alt="Image from Gyazo" width="450"/></a>
  
中身はこのようなものです。JSON という形式で先ほどのノードが示されています。  
```JSON
[{"id":"d82216061e268340","type":"comment","z":"80cc5966bb5f04f3","name":"感知式信号機","info":"","x":90,"y":560,"wires":[]},{"id":"33c441a240ac24bf","type":"obniz-repeat","z":"80cc5966bb5f04f3","obniz":"","name":"","interval":100,"code":"msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納\r\n\r\nreturn msg; //msg.payloadを出力","x":90,"y":620,"wires":[["0475abc22f78c73a"]]},{"id":"0475abc22f78c73a","type":"switch","z":"80cc5966bb5f04f3","name":"","property":"payload","propertyType":"msg","rules":[{"t":"lt","v":"150","vt":"num"},{"t":"gte","v":"150","vt":"num"}],"checkall":"true","repair":false,"outputs":2,"x":190,"y":680,"wires":[["d868b775d6aebf01"],["d8f182c07e576548"]]},{"id":"076fd1f5459975fe","type":"obniz-function","z":"80cc5966bb5f04f3","obniz":"","name":"","code":"\r\nobniz.wait(3000);\r\nobnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる\r\nobniz.wait(5000);\r\nlight.single(\"yellow\");\r\n\r\nreturn msg;\r\n","x":540,"y":640,"wires":[["903c0a52d558bfbc"]]},{"id":"903c0a52d558bfbc","type":"debug","z":"80cc5966bb5f04f3","name":"debug 2","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":720,"y":680,"wires":[]},{"id":"d868b775d6aebf01","type":"change","z":"80cc5966bb5f04f3","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"green","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":360,"y":640,"wires":[["076fd1f5459975fe"]]},{"id":"d8f182c07e576548","type":"change","z":"80cc5966bb5f04f3","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"red","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":360,"y":720,"wires":[["d2b1634250baba16"]]},{"id":"d2b1634250baba16","type":"obniz-function","z":"80cc5966bb5f04f3","obniz":"","name":"","code":"obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる\r\n\r\nreturn msg;","x":540,"y":720,"wires":[["903c0a52d558bfbc"]]}]
```

では今度は、同じハンバーガーメニューから`読み込み`を選択し、先ほど JSON ファイルをアップロードしてみましょう。`読み込むファイルを選択`から先ほどのJSONファイルをアップロードすることができます。    
  
<a href="https://gyazo.com/f4b8e24d03b84a53af0b3fc095caedf9"><img src="https://i.gyazo.com/f4b8e24d03b84a53af0b3fc095caedf9.png" alt="Image from Gyazo" width="600"/></a>

先ほどと同じノードが出現します。  
<a href="https://gyazo.com/357ad4459527efe0e629bcd692de00ec"><img src="https://i.gyazo.com/357ad4459527efe0e629bcd692de00ec.png" alt="Image from Gyazo" width="600"/></a>


##### さて、この JSON 形式のデータを使えると何が嬉しいでしょうか？

一つは今やったように、つくったフローを好きな保存できることでフローを管理することができますね。
  
> [!IMPORTANT]
> もう一つは...そう、生成 AI のプロンプトに入れることができるんですね！！
> この部分は Day2 で触れていくのでお楽しみに！  
  
----  

では次の演習に進んでみましょう。
  
[◀ Lesson1に戻る](../)
