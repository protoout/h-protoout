# 取得した数値データを四捨五入したい: 計算処理いろいろ

温湿度や距離センサー、その他APIで取得したデータが小数点以下の値まで含まれていて、四捨五入や切り捨て・切り上げ等を行いたい場合があると思います。

ここでは距離センサーを用いて、どのように計算処理できるかを説明します。


## 準備: センサーの値やAPIより取得した数値をコンソールに表示する

<a href="https://gyazo.com/5b92d1d7fb36acda099cfc3c2c16b7ad"><img src="https://i.gyazo.com/5b92d1d7fb36acda099cfc3c2c16b7ad.gif" alt="Image from Gyazo" width="500"/></a>


ここでは距離センサーを例に説明します。

[電子パーツの基本的な使い方一覧: 距離センサー](./parts-lib.md#%E8%B6%85%E9%9F%B3%E6%B3%A2%E8%B7%9D%E9%9B%A2%E3%82%BB%E3%83%B3%E3%82%B5%E3%83%BC)



2. obniz repeatノードの設定をひらく

```javascript

msg.payload = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をmsg.payloadに格納

return msg; //msg.payloadを出力

```



3. 四捨五入するように書き換える

四捨五入は、Math.round(X)で計算できます。

- 切り捨て: `Math.floor(x)`
- 切り上げ: `Math.ceil`

```javascript

let distance; //distanceという変数をつかいますよという宣言

distance = await obnizParts.hcsr04.measureWait(); // センサーから取得した値をdistanceに格納

msg.payload = Math.round(distance); //msg.payloadに、distanceを四捨五入したものを格納する

return msg;

```

4. 結果

四捨五入できていればOKです！

<a href="https://gyazo.com/b437db7a1b751d969e367e41ef0b7f3e"><img src="https://i.gyazo.com/b437db7a1b751d969e367e41ef0b7f3e.png" alt="Image from Gyazo" width="500"/></a>



## 四捨五入以外の計算をする

他にも、PIやsin、cos、絶対値、平方根などさまざまな計算ができます。

■ 参考

[JavaScript Mathについて](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Math)

---

**[◀ 目次ページに戻る](../readme.md)**