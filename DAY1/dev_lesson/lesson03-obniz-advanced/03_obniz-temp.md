# 温湿度センサー

### **新しいことをはじめる前に**  

[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。

---

## 1. やってみよう

1. obnizと温湿度センサーを写真のようにつなぐ

温湿度センサーの穴が空いている面からみて、左から0,1,2,3の順で繋いでください。
<a href="https://gyazo.com/e97a9e811cfe8957128826720f509d20"><img src="https://i.gyazo.com/e97a9e811cfe8957128826720f509d20.jpg" alt="Image from Gyazo" width="500"/></a>
<a href="https://gyazo.com/634598ac1868f02bbd4100bd06af5a89"><img src="https://i.gyazo.com/634598ac1868f02bbd4100bd06af5a89.png" alt="Image from Gyazo" width="500"/></a>


※直接obnizにさしても動きますが、少しゆるいためブレッドボードを使います。



2. obniz repeatノードとdebugノードを置き、図のようにつなぐ
<a href="https://gyazo.com/fde72c61d77a840518cbcf1f1122efdf"><img src="https://i.gyazo.com/fde72c61d77a840518cbcf1f1122efdf.png" alt="Image from Gyazo" width="500"/></a>

3. obniz repeatノードのコードを書く
```javascript

msg.payload = await obnizParts.dht20.getAllDataWait();

return msg;

```

4. 初期化処理コードを書き換える

▼初期化処理コード
```json
obnizParts.dht20 = obniz.wired("DHT20",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: "5v"});

```

5. デプロイし、湿度と温度が表示されればOK。
<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>

6. ダッシュボードに数字データを取り出して表示。textノードと直接つなぐと...
<a href="https://gyazo.com/9744219306a9d8d21439cd5f017bf729"><img src="https://i.gyazo.com/9744219306a9d8d21439cd5f017bf729.png" alt="Image from Gyazo" width="622"/></a>

こうなってしまいます。
<a href="https://gyazo.com/bc784ede411be0e701fd0fd9841b88a2"><img src="https://i.gyazo.com/bc784ede411be0e701fd0fd9841b88a2.png" alt="Image from Gyazo" width="408"/></a>


**数字だけを取り出すにはどうしたらいいでしょう？**


### ノードが渡すメッセージ「msg」って何？

Node-REDのノードは、左から右へメッセージ「msg」を渡します。

obniz repeatノードのmsgの中身をみてみましょう。

```json
{"payload":{"humidity":56.6,"temperature":26.78},"_msgid":"33d37c2cab810345"}

```

このような形式のデータをJSONといいます。


図にするとこんな構造になっています。
<a href="https://gyazo.com/4c7275a23caf7364cc657954c89eee47"><img src="https://i.gyazo.com/4c7275a23caf7364cc657954c89eee47.png" alt="Image from Gyazo" width="350"/></a>


今、msgの中のpayloadの中身が丸々テキストに表示されている状態です。
`{"humidity":56.6,"temperature":26.78}`


changeノードをつかって、数字のみの値を渡すようにしましょう！


7. changeノードを配置する

<a href="https://gyazo.com/cb595807ffc979383f0229e15fb991ea"><img src="https://i.gyazo.com/cb595807ffc979383f0229e15fb991ea.png" alt="Image from Gyazo" width="500"/></a>

8. パスをコピーする

<a href="https://gyazo.com/2a4476e189515b7858f6c0bd14e56bbe"><img src="https://i.gyazo.com/2a4476e189515b7858f6c0bd14e56bbe.png" alt="Image from Gyazo" width="312"/></a>

9. changeノードの代入する値を設定する。

msgに変更し、先ほどコピーしたパスを貼り付ける。

<a href="https://gyazo.com/dae413fefd17d4b9911329a1b540db0e"><img src="https://i.gyazo.com/dae413fefd17d4b9911329a1b540db0e.png" alt="Image from Gyazo" width="519"/></a>


### 完成したフロー

```JSON
[{"id":"325b5a769a36c509","type":"obniz-repeat","z":"50bd6451c23b920d","obniz":"a1e02a9aa2adf951","name":"","interval":100,"code":"msg.payload = await obnizParts.dht20.getAllDataWait();\n\nreturn msg;","x":290,"y":260,"wires":[["7fb0eb02ddbb7791","585985d40e3cbfde"]]},{"id":"7fb0eb02ddbb7791","type":"debug","z":"50bd6451c23b920d","name":"debug 1","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":640,"y":260,"wires":[]},{"id":"23e78a3e75e2b351","type":"ui_text","z":"50bd6451c23b920d","group":"4a03c246.55f3d8","order":2,"width":0,"height":0,"name":"","label":"湿度","format":"湿度は、{{msg.payload}}％","layout":"row-spread","className":"","style":false,"font":"","fontSize":16,"color":"#000000","x":690,"y":360,"wires":[]},{"id":"585985d40e3cbfde","type":"change","z":"50bd6451c23b920d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload.humidity","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":480,"y":340,"wires":[["23e78a3e75e2b351"]]},{"id":"a1e02a9aa2adf951","type":"obniz","obnizId":"40725365","deviceType":"obnizboard1y","name":"キサイチ","accessToken":"LU9lVJcNb47aDtOxRk5pPlPCxeiA5ServT8g20LtCOeeEtM2mmgcgqNUglK9gvvo","code":"//obnizParts.hcsr04 = obniz.wired(\"HC-SR04\", { gnd: 0, echo: 1, trigger: 2, vcc: 3 });\nobnizParts.dht20 = obniz.wired(\"DHT20\",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: \"5v\"});\n"},{"id":"4a03c246.55f3d8","type":"ui_group","name":"Default","tab":"ccec3682.947098","order":1,"disp":true,"width":"6","collapse":false},{"id":"ccec3682.947098","type":"ui_tab","name":"Home","icon":"dashboard","order":1}]

```


## 2.演習


### 2-1. 温度も一緒に表示してみよう

同じやり方で、今度は温度の値も並べて表示をしてみましょう。

<a href="https://gyazo.com/8fcb533d6962822527fe9b7bf0c02d59"><img src="https://i.gyazo.com/8fcb533d6962822527fe9b7bf0c02d59.png" alt="Image from Gyazo" width="331"/></a>



### 2-2. 【応用】熱中症アラートを作ってみよう

暑さ指数（WBGT（湿球黒球温度）：Wet Bulb Globe Temperature）を計算し、熱中症アラートを作ってみましょう。

**屋内のWBGT計算式**：WBGT ＝0.7 × 湿球温度 ＋ 0.3 × 黒球温度

[暑さ指数(WBGT)について](https://www.wbgt.env.go.jp/wbgt.php)


※ このセンサーで取得できる温度・湿度は「湿球温度」「黒球温度」とは異なりますが、演習としてチャレンジしてみてください。


---

**[◀ 目次ページに戻る](../readme.md)**