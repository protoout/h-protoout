# チュートリアル1: 温湿度センサーを使用し、熱中症アラートを作ろう



### 完成イメージ

温度と湿度から暑さ指数を計算し、警戒度をLEDで示します。
ドライヤーを吹きかけると、警戒レベルがぐっと上がります。
<a href="https://gyazo.com/5f6bd75cbbe145d6319a105bd3806fdc"><img src="https://i.gyazo.com/5f6bd75cbbe145d6319a105bd3806fdc.gif" alt="Image from Gyazo" width="600"/></a>


### 0. 準備：タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

[停止用ノードはこちら](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)



準備ができたら早速始めていきます！


### 1. 温湿度センサーの値を取得できるようにする

[温湿度センサー](/tools/parts-manual/sensor/temp-hum.md)を参考に温湿度の値を取れるところまで行ってください。

<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>



### 2. 暑さ指数WBGTの計算式


暑さ指数（WBGT（湿球黒球温度）：Wet Bulb Globe Temperature）を温度と湿度から簡易的に計算する方法をつかいます。

- [参考:IchigoJam S+温湿度センサSi7021で暑さ指数WBGTを計算して、熱中症予防](https://bokunimo.net/blog/ichigo-jam/29/)→こちらの記事にはWBGTを簡易的に求める類似式が掲載されています。

```
WBGT = 0.725*Ta + 0.0368*RH + 0.00364*Ta*RH – 3.246

```
Ta=室温（℃）、RH=相対湿度（%）

この式の[MIT LICENSE](https://bokunimo.net/bokunimowakaru/licences/mit_license_2016.txt)


functionノードの中でこの式に温湿度センサーの値を入れて計算し、結果を出力するようにします。


### 3. 暑さ指数WBGTの計算をfunctionノードでできるようにする

まずはfunctionノードを追加。

<a href="https://gyazo.com/bb3b144869fbfe61c17a3e611ea13c58"><img src="https://i.gyazo.com/bb3b144869fbfe61c17a3e611ea13c58.gif" alt="Image from Gyazo" width="500"/></a>

次に、functionノードの中身を書いてもらいましょう。

[プロンプトサンプル](/tools/prompt-sample.md)の、「１. Node-REDのFunctionノードで使えるコードを生成」のプロンプトを書き換えてみましょう。

systemはいじらず、promptのところを書き換えます。

```
## system

- 常にNode-REDのFunctionノードで利用できるコンテンツを返してください。
- 常にvarの代わりにconstかletを使います。
- 外部のノードモジュールを使用するように要求されない限り、require() を使用しないでください。
- 指示がない限り、基本的にコードとインラインコードコメントを返します。

## prompt
- センサーの値が2つ送られてきます。payload.humidity（湿度）、payload.temperature（温度）
- 次の計算を行い、payload.WBGTにWBGTの計算結果を出力してください。 WBGT= 0.725*Ta + 0.0368*RH + 0.00364*Ta*RH – 3.246（Ta=室温（℃）、RH=相対湿度（%））

```

<a href="https://gyazo.com/d38cc786df4a7264050d6fb5dc17f759"><img src="https://i.gyazo.com/d38cc786df4a7264050d6fb5dc17f759.png" alt="Image from Gyazo" width="500"/></a>


試したところ、このようなコードが出てきました。



```javascript
const Ta = msg.payload.temperature; // 室温（℃）
const RH = msg.payload.humidity; // 相対湿度（%）

// WBGTの計算
const WBGT = 0.725 * Ta + 0.0368 * RH + 0.00364 * Ta * RH - 3.246;

msg.payload.WBGT = WBGT; // 計算結果をpayloadに設定

return msg; // メッセージを返す

```

このように、WBGTの値が表示されていればOKです。

※ 生成AIの応答の違いにより、msg.payloadにWBGTのみ表示するコードが出力される場合もあります。プロンプトでより明示的に示してあげると結果が安定します。

<a href="https://gyazo.com/edfcd36252a75692b525347577b7005b"><img src="https://i.gyazo.com/edfcd36252a75692b525347577b7005b.png" alt="Image from Gyazo" width="500"/></a>


### 4. LED信号を光らせる



[信号LED](/tools/parts-manual/Indicator/ledlights.md)の資料を参考に、injectをクリックするとLEDを赤く光るところまで行ってください。

ただし、0〜3番ピンは温湿度センサーで使っているため、信号LEDは8〜11番ピンに刺し、の初期化処理コードも書き換えてください。

■ 初期化処理コードの書き換え

```javascript
obnizParts.dht20 = obniz.wired("DHT20",{vcc:0, sda:1, gnd:2,  scl:3 ,voltage: "5v"}); //0,1,2,3番にピンをアサインし、電圧を5Vに設定
obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:8, green:9, yellow:10, red:11});

```

<a href="https://gyazo.com/fcdf401150b535daed415581192921fb"><img src="https://i.gyazo.com/fcdf401150b535daed415581192921fb.png" alt="Image from Gyazo" width="500"/></a>


### 5. 取得したデータ判定し、下記のようにLED信号を使って表示させましょう。

- 危険: 31以上 →red
- 厳重警戒または警戒: 25以上31未満　→yellow
- 注意: 25未満 →green

[参考: 暑さ指数(WBGT)について](https://www.wbgt.env.go.jp/wbgt.php)

- switchノードを配置し以下のように設定

<a href="https://gyazo.com/ff918a211e74cbdf947ee700d0cf14e1"><img src="https://i.gyazo.com/ff918a211e74cbdf947ee700d0cf14e1.png" alt="Image from Gyazo" width="500"/></a>

<a href="https://gyazo.com/196f7a67c62cd3f0508ab3a0671884bd"><img src="https://i.gyazo.com/196f7a67c62cd3f0508ab3a0671884bd.png" alt="Image from Gyazo" width="500"/></a>


- changeノードとobniz functionノードを配置し、設定する
<a href="https://gyazo.com/56bad58f1106d2ecfb0c48fd66adc6bf"><img src="https://i.gyazo.com/56bad58f1106d2ecfb0c48fd66adc6bf.gif" alt="Image from Gyazo" width="500"/></a>

- changeノードの設定

<a href="https://gyazo.com/2ae458a5b7a00e7198bd8a09d3e87fa6"><img src="https://i.gyazo.com/2ae458a5b7a00e7198bd8a09d3e87fa6.gif" alt="Image from Gyazo" width="500"/></a>

- obniz functionの設定

<a href="https://gyazo.com/09b7e215a391ef378a30d7fa5e2f457f"><img src="https://i.gyazo.com/09b7e215a391ef378a30d7fa5e2f457f.gif" alt="Image from Gyazo" width="500"/></a>

先ほどマニュアルからもってきたobniz functionと同じ内容を記入します。

obniz functionノードをctr + C, ctr+Vしてコピーして使用してもOKです。


### 6. 動作を確かめる

さあ、動かしてみましょう。
<br>
<br>

あれ、動きません。

<br>

switchに入力されているデータが正しいか見てみましょう。

WBGTの数字のみ、switchに入力しなければなりませんが、今は温度、湿度を含むJSONデータを入れてしまっています。

これを修正します。


<a href="https://gyazo.com/5206d38c99fc3cf676eb8fdf3ee8c9a2"><img src="https://i.gyazo.com/5206d38c99fc3cf676eb8fdf3ee8c9a2.png" alt="Image from Gyazo" width="280"/></a>


- changeノードを追加し、設定する

図のようにつなぎ、msg.payloadの値をmsg.payload.WBGTに変更するよう設定してください。

<a href="https://gyazo.com/3c062387b7b8814f3686ab16a8f481f0"><img src="https://i.gyazo.com/3c062387b7b8814f3686ab16a8f481f0.gif" alt="Image from Gyazo" width="600"/></a>


### 7. 動作を確かめる！

もう一度デプロイして確かめましょう。

ライトが光ればOKです。

温湿度センサーに向かってハァ〜〜〜と息を吹きかけて温めると、LEDの色が変わります。

---

**[◀ 目次ページに戻る](../readme.md)**