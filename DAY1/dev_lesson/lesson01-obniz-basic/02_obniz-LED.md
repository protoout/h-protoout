# Lチカ（LED をチカチカ光らせる）してみよう

## LED を使いますがその前に...  

### 【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意
> [!WARNING]
> **極性に注意！**  
> 扱うセンサーやアクチュエーターは極性があるかないか（プラスマイナスの電流の向き）を注意しましょう  
> 極性を間違えて配線をするとデバイスが熱を持って高温になったり、壊れたりする場合があります
>   
> **怪我・破損注意！**  
> 扱い方を間違える怪我や火傷をする場合や、デバイスが壊れる場合があります。注意レベルを上げましょう。
obniz本体やパーツが熱くなっている場合があります。取り外す場合は注意しましょう。
>    
> **プログラムを起動しっぱなしにしない**  
> プログラムを起動したまま≒電気が通電しっぱなしの状態です。センサーなどがショートしてしまって破損や怪我に繋がる恐れがあります。
別のセンサーやアクチュエーターを試す際は、 必ず一度でプログラムを停止させてから、付け替えるようにしましょう。
新たなプログラムを起動する際は、毎回必ずobnizディスプレイにQRコードとobniz IDが表示されていることを確認してください。


### 壊してしまった場合  
気にしないでください！たいてい誰でも1回は壊します。パーツ自体はそれほど値段もしないので、勉強代と思っていきましょう。  

----  

## LEDをつけてみましょう
  
信号機などでおなじみのLEDです。

<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="30%" />
  
青と赤の好きな方を選んでください！

  
### 1. obniz Board での配線

> [!WARNING]
> **極性(+ -)があるため、接続に間違いがないか注意**  
> LED は **Light Emitting Diode**（光を出すダイオード）の略称です。  
> ダイオードとは、電流を一方向にしか流さない半導体部品のことです。  
> したがって、正しくピンを配置する必要があります。  
  
<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" width="40%" />

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| LEDの長い脚（+端子）  | obnizの0番    |
| LEDの短い脚（-端子）  | obnizの1番    |

  

### 2. 使うノードとつなぎ方
    
- `injectノード`
- `obniz-functionノード`

<img src="https://i.gyazo.com/590a12c00834a74480a8e79cdf270b7e.png" width="40%" />

先ほどまでやっていた処理の下に追加していきましょう。  
<a href="https://gyazo.com/3b013b1f8d811462555883f1d483f469"><img src="https://i.gyazo.com/3b013b1f8d811462555883f1d483f469.png" alt="Image from Gyazo" width="450"/></a>

> [!TIP]
> 上記のようにノードを整理するために `commentノード`も使いましょう  
> <a href="https://gyazo.com/548a1a7c150e5c5764e2b13e9c8efcfb"><img src="https://i.gyazo.com/548a1a7c150e5c5764e2b13e9c8efcfb.png" alt="Image from Gyazo" width="450"/></a>



### 3. 初期化処理コードの編集
`obniz functionノード`のペンマークのところを押すと初期化処理を書くことができます。  
> <a href="https://gyazo.com/60bf95ddfcaf54e7d79c9c7cd260314a"><img src="https://i.gyazo.com/60bf95ddfcaf54e7d79c9c7cd260314a.png" alt="Image from Gyazo" width="450"/></a>
<br>

> [!IMPORTANT]
> ここで「＋」マークから新たに Obniz 設定ノードを追加する必要はないので注意しましょう！
> ひとつ前の演習でつくった Obniz Board の ID を選びましょう。

```js
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 }); //脚の長い方（アノード, +）を0, 脚の短い方（カソード,-）を1に割り当てる
```

書き終えたら「更新」を忘れずに！  
  
### 4. 各ノードの設定方法

#### 4-1. 単純な点灯

- `obniz-functionノード`のコード

```js
obnizParts.led.on(); //ledをONにする

return msg;
```

準備ができたら実行してみましょう！  
  
#### 4-2. 消灯

- `obniz-functionノード`のコード

```js
obnizParts.led.off(); //ledをONにする

return msg;
```

準備ができたら実行してみましょう！  
  
#### 4-3. 単純な点滅

- `obniz-functionノード`のコード

```js
obnizParts.led.on(); //ledをONにする
obniz.wait(1000); //1秒(1000ミリ秒)待つ
obnizParts.led.off(); //ledをONにする

return msg;
```
  
準備ができたら実行してみましょう！  
  
### 5. 結果

点灯、消灯、点滅ができたら OK です！

> [!CAUTION]
> **`obniz-close` で停止するのをお忘れなく！**
> 停止をしたら obniz Board がこの画面になるので、そうしたらパーツを外しましょう。  
> <a href="https://gyazo.com/ae81bec5f4c3e1ffda2b33be422469de"><img src="https://i.gyazo.com/ae81bec5f4c3e1ffda2b33be422469de.jpg" alt="Image from Gyazo" width="450"/></a>



----  

## 💡Lチカなんです！💡
> [!TIP]
> ソフトウェアの世界では一番最初に書く最も簡単なコードのことを「Hello World」と言いますが、ハードウェアの世界ではLEDを点滅させる「**Lチカ**」がそれに相当します。  
> **LEDをチカチカさせること** です

**ハードウェアの世界に一歩足を踏み入れましたね🎊**

では次に進みましょう！

----  
  
[◀ Lesson1に戻る](../)
