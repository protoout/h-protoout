# obnizで複数のパーツを同時に使いたい

ここではobnizで複数のパーツを同時に使うときの手順を説明します。

- [1つのセンサーと1つのアクチュエーターまたはインジケーターを同時に使用する場合](./obniz-multiple-parts.md#1-1つのセンサーと1つのアクチュエーターまたはインジケーターを同時に使用する場合)
- [2つ以上のセンサーを同時に使用する場合](./obniz-multiple-parts.md#2-2つ以上のセンサーを同時に使用する場合)

に分けて説明をしています。

## 1. 1つのセンサーと1つのアクチュエーターまたはインジケーターを同時に使用する場合

1. 配線します


<a href="https://gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef"><img src="https://i.gyazo.com/6403c17f9cdf46fd6fd57d09e6490eef.jpg" alt="Image from Gyazo" width="300"/></a>

- obniz 0 - 電圧出力（5V） 
- obniz 1 - 電圧入力  
- obniz 2 - 電圧出力（0V） 
- obniz 9 - スピーカー
- obniz 11 - スピーカー


2. 初期化処理コードでピンアサインする

obnizでは、何番のピンに何を割り当てるかを初期化処理にかいて設定します。

このとき、必ずピンが被らないようにしてください。


```javascript
obniz.io0.output(true); //電圧出力（5V）用。io0を5vに
obniz.io2.output(false); //電圧出力（0V）用。io2をGNDに
obnizParts.Speaker = obniz.wired("Speaker",{ signal:9, gnd:11 });//9、11番をスピーカーに

```

---



## 2. 2つ以上のセンサーを同時に使用する場合

センサーの値を取得し続けるときに、**obniz repeatノード**を使用します。


使い方に注意が必要です。**obniz repeatノードは、一度に1つまで** にする必要があります。



**同時に複数のobniz repeatノードを動かすと、おかしな挙動になります。**


ここでは、複数のセンサーを使用するときの方法について説明します。


1. 使いたいセンサー2つを配線してください。ここではCdSと温湿度センサーの2つを使用します。



2. obniz repeatのコードを1つにマージする

[電子パーツマニュアル](./parts-manual/)から、obniz repeatノードのコードをそれぞれ抜き出してみます。


**1つめのセンサー（温湿度センサー）**

```javascript

msg.payload = await obnizParts.dht20.getAllDataWait();
return msg;

```


**2つめのセンサー（CdS）**

```javascript

var voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

msg.payload = voltage; 

return msg;


```

↓

↓ この2つのコードを1つのコードにマージします

↓ 🖊🍍🍎🖊（イメージ）


#### マージした結果: NG例


```javascript

msg.payload = await obnizParts.dht20.getAllDataWait(); //温湿度センサーの値をmsg.payloadに格納

var voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

msg.payload = voltage; //2行目のCdSの値をmsg.payloadに格納する: 温湿度センサーの値は上書きされて消える

return msg;

```

この書き方だと、せっかく取得した温湿度センサーの値が、CdSの値で上書きされてしまい、CdSの値しか出力しません。


#### マージした結果: OKな例

msg.payloadの中に、cdsという名前のついた小さい箱を入れてその中にCdSのデータを格納してあげましょう。

下記のように変更します。


- 2つ目のmsg.payload → msg.payload.cds


※「.」以下は任意の名前をつけることができます。



```javascript

msg.payload = await obnizParts.dht20.getAllDataWait(); //温湿度センサーの値をmsg.payloadに格納

var voltage = await obniz.ad1.getWait(); //ピン1からアナログ（光の強さ）をデジタル信号に変換した値を取得

msg.payload.cds = voltage; //2行目のCdSの値をmsg.payloadに格納する: 温湿度センサーの値は上書きされて消える

return msg;

```

3. このような結果が出れば成功です

```json
{cds: 000, humidity:000, temperature: 000}

```

ここから、CdSの値だけ、温度だけ、湿度だけなど欲しいデータだけを取り出す方法は、

- [データの中から特定の数値のみ取り出して使うには？ changeノードを使ってJSONデータを扱う](./json-data.md)

を参照してください。


---

**[◀ 目次ページに戻る](./readme.md)**
