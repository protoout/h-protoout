# チュートリアル1: サーボモーターでピョコピョコ連続で動かす

30度と90度を繰り返してぴょこぴょこうごかすものをつくります。

### 完成イメージ

<a href="https://gyazo.com/394dc1a4ae1acda14235efdf4a06014d"><img src="https://i.gyazo.com/394dc1a4ae1acda14235efdf4a06014d.gif" alt="Image from Gyazo" width="376"/></a>


### 1. サーボモーターをピョコピョコ連続で動かそう

#### 1. [電子パーツの使い方一覧](../parts-manual/servo.md)を参考に、injectノードのボタンをクリックするとサーボモーターが動き、コンソールに現在の角度が表示される状態まで作ってみます。

マニュアルでは`chagneノード`を使っていましたが、こちらでは`ingectノード`に値を入れてみます。

<a href="https://gyazo.com/386a1d891e3183372b7ee03d7ad49881"><img src="https://i.gyazo.com/386a1d891e3183372b7ee03d7ad49881.gif" alt="Image from Gyazo" width="500"/></a>

msg.payloadの項目を数値にして画像のように設定してみましょう。

<a href="https://gyazo.com/07730ffe37a53eb5df08aeb35f617eec"><img src="https://i.gyazo.com/07730ffe37a53eb5df08aeb35f617eec.png" alt="Image from Gyazo" width="500"/></a>



#### 2. 30度と90度を繰り返すとはどういうことか？考えてみる。

30度になったら90度にする
90度になったら30度にする

30度に動かす→ 30を出力する→ 30の場合90を出力する
90度に動かす→90を出力する→ 90の場合30を出力する

これを交互に繰り返す......

#### 3. 使うノードを考えてみる

- 「もし、◯◯だったら...」　→ switchノードを使う

- 「msg.payloadに△△を出力したい」→ changeノードを使う

#### 4. 「もし、30度だったら、90を出力する」まで作ってみる

もし、30度だったら（switch）、90を出力する(change)
<a href="https://gyazo.com/f3a5ffbc32d891788e4b48ed96d90d42"><img src="https://i.gyazo.com/f3a5ffbc32d891788e4b48ed96d90d42.png" alt="Image from Gyazo" width="985"/></a>


- switchとchangeの設定

<a href="https://gyazo.com/678f37f841496146e24fcca4065847fb"><img src="https://i.gyazo.com/678f37f841496146e24fcca4065847fb.gif" alt="Image from Gyazo" width="500"/></a>

★ changeノードは、プルダウンから「数値」に変更するのを忘れずに！



injectノードの30をクリックすると、サーボモーターが30度に動き、90という数字を出力するようになればOK

<a href="https://gyazo.com/f393ddc1b19b911bcbbb9a462b44fdd0"><img src="https://i.gyazo.com/f393ddc1b19b911bcbbb9a462b44fdd0.gif" alt="Image from Gyazo" width="1000"/></a>


#### 5. 「もし、90度だったら、30を出力する」を作ってみる

- changeノードを追加して、30を出力するようにする

<a href="https://gyazo.com/3e10941588631ad98c3d940c06aa3b76"><img src="https://i.gyazo.com/3e10941588631ad98c3d940c06aa3b76.gif" alt="Image from Gyazo" width="1000"/></a>


- switchノードに、90度だった場合の分岐を増やし、図のように接続する

<a href="https://gyazo.com/e56716f61e53e21847b793217b913118"><img src="https://i.gyazo.com/e56716f61e53e21847b793217b913118.gif" alt="Image from Gyazo" width="1000"/></a>



- changeノードの出力を、obniz functionの入力につなげる

<a href="https://gyazo.com/fd1ed92f3b56736261d0ab5894ee03f6"><img src="https://i.gyazo.com/fd1ed92f3b56736261d0ab5894ee03f6.png" alt="Image from Gyazo" width="880"/></a>


#### 6. 試してみる

injectノードをクリックすると、その後は自動でサーボモーターが繰り返し動くことを確かめてください。

<a href="https://gyazo.com/30d5f5536f95eb1170a7b061ff8c4f71"><img src="https://i.gyazo.com/30d5f5536f95eb1170a7b061ff8c4f71.gif" alt="Image from Gyazo" width="784"/></a>


.....？？？？

<br>
<br>

でも何かがおかしいですね。


角度が、30度と90度を行き来するはずが、均等でなく角度も変です。


<br>
<br>

なぜでしょう？？？

<br>
<br>


サーボモーターが30度または90度に動き切る前に、changeノードがサーボモーターを動かす指示を与えてしまっているせいではないでしょうか。


このように、アプリケーション上での動きだけでなく、物理的にどのような現象が起こっているかも考える必要があります。


#### 7. changeノードからのサーボモーターを動かす指示を遅らせる


delayというノードがあります。これを使うと、処理を指定した時間待ってくれます。

changeノードとobniz functionの間にdelayノードを入れます。

<a href="https://gyazo.com/87935d46015b8016aa74c8313724ec3b"><img src="https://i.gyazo.com/87935d46015b8016aa74c8313724ec3b.png" alt="Image from Gyazo" width="645"/></a>


時間を`0.5`に変更

<a href="https://gyazo.com/961afe1e36caa7484773b9a9f9053912"><img src="https://i.gyazo.com/961afe1e36caa7484773b9a9f9053912.gif" alt="Image from Gyazo" width="704"/></a>



#### 8. 再度試してみる

いかがでしょう？

今度はきちんと30度と90度を行き来しています。

<a href="https://gyazo.com/394dc1a4ae1acda14235efdf4a06014d"><img src="https://i.gyazo.com/394dc1a4ae1acda14235efdf4a06014d.gif" alt="Image from Gyazo" width="376"/></a>


### 2. 箱を開けたらピョコピョコ動かすトリガーをつくる

マウスのクリックにより、サーボモーターが動き始めるようになっていますが、

今度は、センサーの値をトリガーとして動き始めるように作り変えてみましょう。


**箱を開けたらサーボモーターがぴょこぴょこうごき、閉じたら止まる**


この状態を目指します。



今回は[超音波距離センサー](../parts-manual/sensor/distance.md)を使って、箱が空いたか閉じたかを判定します。


#### 1. obnizに超音波距離センサーを接続し、値を取得できるようにする

[超音波距離センサー](../parts-manual/sensor/distance.md)を参考に、まずは接続して超音波距離センサーの値を取得できるところまで行ってください


ピンが4つ必要です。今回はマニュアルと同じく8,9,10,11番のピンを使ってみます。

複数の電子パーツを使うときのやりかたは、[obnizで複数のパーツを同時に使いたい](../obniz-multiple-parts.md)を参照してください。


■ 初期化処理コード

```javascript

obnizParts.hcsr04 = obniz.wired("HC-SR04",{ gnd:8, echo:9, trigger:10, vcc:11 });
obnizParts.servo = obniz.wired("ServoMotor", { signal: 2 });

```

フロー

<a href="https://gyazo.com/1391dcbfb2da41499acae85afeebbc91"><img src="https://i.gyazo.com/1391dcbfb2da41499acae85afeebbc91.png" alt="Image from Gyazo" width="915"/></a>



#### 2. 距離センサーの値による分岐処理を書く

箱の開け閉めを取得し、出力が変わるようにしましょう。

Switchノードをつなげ、設定してください。とりあえず50mmを境に分岐させたいと思います。

分岐を2つ作り、「数値」「50」と入力してください。

<a href="https://gyazo.com/bd45c2aa91bf040c3919ec7c68f497c4"><img src="https://i.gyazo.com/bd45c2aa91bf040c3919ec7c68f497c4.gif" alt="Image from Gyazo" width="600"/></a>


#### 3. 動きを止めるにはどうすればいいか考える① うまくいかない例

現在は、30または90を入力すると、その後は自動で動き続ける仕様になっています。

止めるためにはどうしたらいいでしょう？

<br>
<br>
<br>


30・90以外の数値を入れれば、止まるはず!

0を出力するinjectノードを1つ追加して、obniz functionにつなぎ実験してみましょう。

<a href="https://gyazo.com/1f72638606c603b71e232bcb90e32d24"><img src="https://i.gyazo.com/1f72638606c603b71e232bcb90e32d24.png" alt="Image from Gyazo" width="612"/></a>

<br>
<br>

結果: **サーボモーター、止まらない!!!**

全然、止まりませんでした。なぜでしょうか。


現在のフロー設計では、0が入力されても、すでに次の繰り返し処理（30や90）がスケジュールされてしまっているのでしょう。



#### 4. 動きを止めるにはどうすればいいか考える② うまくいく例

サーボモーターを交互に動かす機能と、これ自体をON/OFFする機能を分けて考えてみましょう。

- ONの状態だったら、サーボモーターを繰り返し動かす
- OFFの状態だったら、サーボモーターの動きを停止させる


ON/OFFの状態管理を行うのに、flowオブジェクト: `flow.payload`を使用してみます。


- msgオブジェクト: 今までみなさんが使っている `msg.payload`。つながっているノード同士で保持されるデータ。
- flowオブジェクト: 同一のタブ（フロー、サブフロー）単位で保持、維持されるオブジェクト。`flow.payload` で値の参照や上書きができます。


1. 下記のように組んでみましょう

- flow.payloadがtrueだったら、サーボモーターを動かし続ける
- flow.payloadがfalseだったら、サーボモーターの動きを止める


switchノードと、changeノード2つをつなぎ、それぞれ設定してください。


- switch

<a href="https://gyazo.com/4d8fa45257300048d980482dd30eb484"><img src="https://i.gyazo.com/4d8fa45257300048d980482dd30eb484.gif" alt="Image from Gyazo" width="500"/></a>


- change

<a href="https://gyazo.com/51063285ffb82611abfd5cd27d52ba65"><img src="https://i.gyazo.com/51063285ffb82611abfd5cd27d52ba65.gif" alt="Image from Gyazo" width="500"/></a>


<br><br><br>

2. サーボモーターを動かすフローにswitchを追加し、設定する

- switch

<a href="https://gyazo.com/96ad9cebd0364a794d7a96eec5699fb4"><img src="https://i.gyazo.com/96ad9cebd0364a794d7a96eec5699fb4.png" alt="Image from Gyazo" width="967"/></a>


設定は以下のように行ってください。




現在のフロー
<a href="https://gyazo.com/01523e79c0a8b7a6c50f7b1326d8dc16"><img src="https://i.gyazo.com/01523e79c0a8b7a6c50f7b1326d8dc16.png" alt="Image from Gyazo" width="500"/></a>



injectの20をクリックするとモーターが止まり、injectの60をクリックしてから、サーボモーターのinjectノードをクリックすると動きつづけることを確認してください。


#### 5. センサーと連動させる

では距離センサーの値と連動させてみましょう！

1. まずは距離センサーを取得するフローを移動してください

<a href="https://gyazo.com/83319e9e89393a9b975c7a82a2ee521b"><img src="https://i.gyazo.com/83319e9e89393a9b975c7a82a2ee521b.png" alt="Image from Gyazo" width="903"/></a>

2. 


---

**[◀ 目次ページに戻る](../readme.md)**