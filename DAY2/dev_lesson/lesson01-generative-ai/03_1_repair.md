# L01-3 - 生成AIでNode-RED: ChatGPTで0からフローを作って改善してみる

先ほどは`Functionノード`の中で使えるコードを生成しましたが、Node-REDで使えるフローを0から生成して機能追加していくこともできます。

## ここでやること

**超音波距離センサーで距離を測ってLEDのオンオフ制御**を作ってみます。

- ChatGPTに指示を出してフローの改善をしてもらいましょう。

### 配線準備

超音波距離センサーとLEDを配線しましょう

> 例えば超音波距離センサーを`0,1,2,3ピン`に,LEDの+(足が長い方)を`4ピン`に、-(足が短い方)を`5`ピンになど接続してください。
> 
> <img src="https://i.gyazo.com/91fb4bbfc54848ecf60f22344cae6905.jpg" width="400px" />


## 1. GPTに指示を出してフローを作ってもらう。

プロンプトサンプルから[Node-REDでobnizノードを動かしたいプロンプトサンプル](../../../tools/prompt-sample.md)の中身をコピペしてChatGPTのチャット画面に貼り付けて命令を出してみましょう。

> <img src="https://i.gyazo.com/d5cf7e2da38f926a05f0ac3ae5c26177.png" width="400px" />
> 
> [実際のイメージ](https://chat.openai.com/share/e/b521826e-d0f4-46f3-83f7-4c9fd61c83ae)

JSONが出力されると思います。

## 2. フローの読み込み

メニュー（右上のメニューか、フロー画面を右クリックして出てくるメニューの挿入項目）からフローの読み込みをします。

ChatGPTによって生成されたJSONを貼り付けて読み込んでみましょう。

> <img src="https://i.gyazo.com/8c68512ef8d66a0972ce6f3572f31d4f.png" width="400px" />

おそらく読み込まれると以下のようなフローが読み込まれると思います。

> <img src="https://i.gyazo.com/26d8e08309cc4133cd205cbad863cd4b.png" width="400px" />


<details><summary>おそらくこんなJSON - クリックで開く</summary>

参考程度です。ここからコピペしないでください。ChatGPTに命令を出して出てきたJSONを各自使ってみましょう。

```json
[ { "id": "obniz-setup", "type": "obniz", "z": "flow-id", "name": "obniz Setup", "code": "obnizParts.hcsr04 = obniz.wired(\"HC-SR04\", {gnd:0, echo:1, trigger:2, vcc:3});\nobnizParts.led = obniz.wired(\"LED\", {anode:4, cathode:5});", "config": "", "x": 220, "y": 140, "wires": [] }, { "id": "obniz-repeat", "type": "obniz-repeat", "z": "flow-id", "name": "obniz Repeat", "interval": "1000", "x": 240, "y": 240, "wires": [ [ "distance-compare" ] ] }, { "id": "distance-compare", "type": "function", "z": "flow-id", "name": "Distance Comparison", "func": "msg.payload = msg.payload < 200; // Check if distance is less than 200cm\nreturn msg;", "outputs": 1, "noerr": 0, "x": 460, "y": 240, "wires": [ [ "led-control" ] ] }, { "id": "led-control", "type": "obniz-function", "z": "flow-id", "name": "LED Control", "code": "if (msg.payload) {\n    obnizParts.led.on();\n} else {\n    obnizParts.led.off();\n}", "config": "", "x": 680, "y": 240, "wires": [] } ]
```

</details>

もう使えそうな形のJSONが出力されました。

## 3. 中身を確認

完璧な状態だと、3つの各ノードの中に以下のコードが記述されています。

- `obniz repeatノード`(左側)

```js
msg.payload = await obnizParts.hcsr04.measureWait();
return msg;
```

- `Functionノード`(真ん中)

```js
if (msg.payload <= 200) {
    msg.payload = true;
} else {
    msg.payload = false;
}
return msg;
```

- `obniz funcionノード`(右側)

```js
if (msg.payload === true) {
    obnizParts.led.on();
} else {
    obnizParts.led.off();
}
```

## 4. 中身の不備を指摘する

ただ、出力されたフローの中にたまに、コードの記述が入ってない場合があります。（講師側のプロンプトエンジニアリング力が足りてないだけかもしれません）

> 色々足りてない
>
> <img src="https://i.gyazo.com/3e9a49f8a2fd53f4651d37ccb85ae018.png" width="400px" />

そんな場合はChatGPTに追加で要望を出しましょう。

[距離センサーのマニュアルページ](../../../tools/parts-manual/sensor/distance.md)を見つつ、コードの指示などを追加依頼します。

> ![](https://i.gyazo.com/8d6a4140b47dd6f94a07b5ea548769ba.png)

理想的な状態になるまで、 **指示を出してJSONを出力して、読み込んで確認して......を繰り返してみましょう。**

やりとりをしているとGPTも覚えてきて精度が上がります。

間違っていたら間違っていると教えてあげましょう。

## 5. 良い結果が出たら設定ノードを更新してデプロイ

何回か試して、イメージする結果ができました。

> ![](https://i.gyazo.com/8e5f186b721b2d5807c578f618099997.png)

最後にobnizの`設定ノード`の初期化処理コードを設定もしくは更新をして実行してみましょう。




> <img src="https://i.gyazo.com/c31a203fb0737f98d925d6d157b58cca.png" width="400px" />


## 

プロンプトを少し覗いてみますが、

[やりとりしていたチャット](https://chat.openai.com/share/e/464b0669-58be-44c3-accd-e12d3a7ee4d7)を見てみます。

> <img src="https://i.gyazo.com/1238ab9dfa8a640d9bb5c2a3196d7add.png" width="400px" />


**[◀ 目次ページに戻る](../readme.md)**