# チュートリアル2: サーボモーターとCdSで明るくなったら90度、暗くなったら0度になるものをつくろう


Day1のPrototypingのときに受講生が作っていたものをチュートリアル化しました。


### 完成イメージ

明るいとサーボモーターが90度、暗いと0度になります。

<a href="https://gyazo.com/371d98adc6a3a8e67e192c4132de5cd2"><img src="https://i.gyazo.com/371d98adc6a3a8e67e192c4132de5cd2.gif" alt="Image from Gyazo" width="472"/></a>


### 0. 準備：タブを追加し、停止用ノードを読み込む
前回のおさらいとなります。


1. +ボタンを押し、新しくできたタブをダブルクリック
<img src="https://i.gyazo.com/bfad18055e1a4119eed4b11e5d1dfad9.png" alt="Image from Gyazo" width="500"/>


2. タブの名前を「obniz-LED」など、わかりやすく編集してください。
<img src="https://i.gyazo.com/19ccf6eaf3e5083bd0c978bf419c61a0.png" alt="Image from Gyazo" width="500"/>

3. 停止用ノードを読み込む

[停止用ノードはこちら](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)



準備ができたら早速始めていきます！


### 1. CdSの値を取得できるようにする

[パーツマニュアル: CdS](/tools/parts-manual/sensor/cds.md)を参考に値を取れるところまで行ってください。



### 2. サーボモーターが動くようにする 

[サーボモーター](/tools/parts-manual/actuator/servo.md)を参考にサーボモーターを動かすところまで作ってください。

★ CdSとピンが被らないように刺し、初期化コードを書き換えするのを忘れずに！


<a href="https://gyazo.com/14ba2bdd0b67153ce361f7eafd63833b"><img src="https://i.gyazo.com/14ba2bdd0b67153ce361f7eafd63833b.png" alt="Image from Gyazo" width="500"/></a>


### 3. CdSの値とサーボモーターの動きを連動させる

下記のようにCdSの値によってサーボモーターの角度が変わるように変更します。

- 明るいとき（CdSの値が0.2以上）: **サーボモーターを90度に動かす**
- 暗いとき（CdSの値が0.2より小さい）: **サーボモーターを0度に動かす**

※ CdSの値のしきい値の設定（どこを境に明るい・暗いとするか）は、環境や抵抗値によって変わりますので、ご自身のデータを見て決めてください。


- switchノードと2つのchangeノードを配置し、設定する
<a href="https://gyazo.com/74d432a2c47f9c715674fc5b8355e7ac"><img src="https://i.gyazo.com/74d432a2c47f9c715674fc5b8355e7ac.gif" alt="Image from Gyazo" width="500"/></a>
 

 switchでは2つの分岐を作ります。

- 1つめの分岐: 明るいとき（CdSの値が0.2以上）: `=>`、`数値`を選択し、`0.2`を入力。
- 2つめの分岐: 暗いとき（CdSの値が0.2より小さい）: `<`、 `数値`を選択し、`0.2`を入力


※ ここでは、0.2を境に明るい/暗いの分岐をさせていますが、**CdSの値は環境や抵抗値によって変わります**ので、`0.2`という部分は実際にCdSの出力結果を見て**ちょうどよい数字に変更してください。**

<a href="https://gyazo.com/e66bf8be71578aaa5d9c0b5b61446cce"><img src="https://i.gyazo.com/e66bf8be71578aaa5d9c0b5b61446cce.gif" alt="Image from Gyazo" width="500"/></a>


changeノードの設定は以下の通りです。

<a href="https://gyazo.com/f5da50713e46ce63fb62abc3e5191a60"><img src="https://i.gyazo.com/f5da50713e46ce63fb62abc3e5191a60.gif" alt="Image from Gyazo" width="500"/></a>


### 4. 動作を試す

ここまでできたらデプロイし、明るさの違いによってサーボモーターの角度が変われば成功です！

<a href="https://gyazo.com/371d98adc6a3a8e67e192c4132de5cd2"><img src="https://i.gyazo.com/371d98adc6a3a8e67e192c4132de5cd2.gif" alt="Image from Gyazo" width="472"/></a>


---

**[◀ 目次ページに戻る](../readme.md)**