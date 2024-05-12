# チュートリアル1: サーボモーターでピョコピョコ連続で動かす


30度と90度を繰り返してぴょこぴょこうごかすものをつくります。



### 完成イメージ

<a href="https://gyazo.com/394dc1a4ae1acda14235efdf4a06014d"><img src="https://i.gyazo.com/394dc1a4ae1acda14235efdf4a06014d.gif" alt="Image from Gyazo" width="376"/></a>


### やってみよう


#### 1. [電子パーツの使い方一覧](./parts-lib.md)を参考に、injectノードのボタンをクリックするとサーボモーターが動き、コンソールに現在の角度が表示される状態まで作る。

<a href="https://gyazo.com/07730ffe37a53eb5df08aeb35f617eec"><img src="https://i.gyazo.com/07730ffe37a53eb5df08aeb35f617eec.png" alt="Image from Gyazo" width="500"/></a>



#### 2. 30度と90度を繰り返すとはどういうことか？考えてみる。

30度になったら90度にする
90度になったら30度にする

30度に動かす→ 30を出力する→ 30の場合90を出力する
90度に動かす→90を出力する→ 90の場合30を出力する

これを交互に繰り返す......

#### 3. 使うノードを考えてみる

「もし、◯◯だったら...」　→ switchノードを使う
「msg.payloadに△△を出力したい」→ changeノードを使う

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


でも何かがおかしいですね。


角度が、30度と90度を行き来するはずが、均等でなく角度も変です。




なぜでしょう？？？




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

---

**[◀ 目次ページに戻る](../readme.md)**