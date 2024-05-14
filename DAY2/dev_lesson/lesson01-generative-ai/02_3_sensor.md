# L01-生成AI: 生成AIと一緒にNode-REDでIoT開発 3/3

引き続きやっていきます。ここではいよいよセンサーに接続してみます。

## 3. 距離センサーが反応したら音を出す

### 3-1. 距離センサーとスピーカーの配線

※**ここからは2人1組でセンサーは貸し合って試してみてください。**

`0,1,2,3ピン`に超音波距離センサー、`9,11ピン`にスピーカーを写真のように配線してみましょう。

> <img src="https://i.gyazo.com/53bb7be7ba1d99ed2934715654e4b1f3.png" width="400px" />
> 
> 見にくくてすみません。

### 3-1. 距離センサーに差し替え

エミュレートで使っていた`Injectノード`,`Changeノード`を`obniz repeatノード`に入れ替えましょう。

> <img src="https://i.gyazo.com/d4fb9397dff4fbfcf93c7f26d5da1117.png" width="400px" />

次に、[超音波距離センサーのマニュアルページ](../../../tools/parts-manual/sensor/distance.md)を参考に`設定ノード`の初期化処理の箇所と`obniz repeatノード`に中に以下の内容をコピペします。

- `1.`: `設定ノード`の初期化処理

```js
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //0,1,2,3番にピンを割り当てる
```

- `2.`: `obniz repeatノード`にコードを記載

```js
msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力
```

- `3.`: obniz IDの設定を忘れずに

また、デプロイする前に`obniz ID`が自身のobnizのものにセットされているかも確認しましょう。セットされていなければセットしてください。

> <img src="https://i.gyazo.com/fac1a5126566311c0e9788b33a0816f8.png" width="400px" />

デプロイして試してみます。距離センサーに手を近づけたりすると、デバッグノードで変化がわかります。

> <img src="https://i.gyazo.com/56b3c520396c384bbc241c2e9d05d9d4.gif" width="400px" />

これで距離センサーから値を取れました。

### 3-2. スピーカーから音を鳴らす

音を鳴らしてみます。

エミュレートで使っていた`Templateノード`を`obniz functionノード`に入れ替えましょう。

次に、[スピーカーのマニュアルページ](../../../tools/parts-manual/actuator/speaker.md)を参考に`設定ノード`と`obniz functionノード`を更新します。

`obniz functionノード`はtemplateノード同様に二つ用意して線で繋ぎます。

> <img src="https://i.gyazo.com/98af8e97befeb2e693aecf6ddc398ef7.png" width="400px" />


- `1.`: `設定ノード`の初期化処理を**更新**

**※注意ポイント**

今回は超音波センサーとスピーカーを両方使うので、初期化処理は以下のようになります。
ピンアサインも気をつけましょう。

```js
obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:0, echo:1, trigger:2, vcc:3 }); //0,1,2,3番にピンを割り当てる
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 }); //←追加
```

- `2.`: `obniz functionノード`1つ目

音を鳴らす処理です。

```js
obnizParts.Speaker.play(1000); // 1000Hz で音を鳴らす
await obniz.wait(1000); //1秒待つ
```

- `3.`: `obniz functionノード`1つ目

音を止める処理です。

```js
obnizParts.Speaker.stop(); // 音を止める
```

- `4.` obniz IDのせずに

Speakerの処理をしている`obniz functionノード`もobniz IDの設定を忘れずにしましょうl。

### 3-3. 実際に動かしてみる

さて、デプロイしてみます。

問題なくいくと以下のように距離に応じて音が鳴ったり止まったりしてくれます。

> [<img src="https://i.gyazo.com/b8d54909da2960018e032e9b4df4e863.png" width="400px" />](https://twitter.com/n0bisuke/status/1789748155984052702)
> 手をかざすと音が鳴って、手を遠ざけると音が止まる

### 3-4. 最終系

こんな感じでステップを踏んでフローを変えてきたイメージがなんとなく掴めていると嬉しいです。

> <img src="https://i.gyazo.com/fbdcafe1eacd1e10bb644d620ab35a4a.png" width="400px" />

### 3-5. ここでのポイントとまとめ

ここまでお疲れ様でした。以下の内容を学べたので制作の時に参考にしてみてください。

- ChatGPTにプロンプトを指定して聞くとFunctionノードで使えるコードが出力されて、機能追加なども日本語の指示で行えます。
- `Injectノード`,`Changeノード`,`Templateノード`でセンサーを繋がなくてもエミュレートができる。
    - これはチームで分担する時に使えます。
- obnizノードの`設定ノード`は2つのセンサーやあくちゅなどを組み合わせるときは上書きではなく更新なので注意しましょう。

**[◀ 目次ページに戻る](../readme.md)**