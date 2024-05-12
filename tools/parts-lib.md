# 電子パーツの基本的な使い方一覧

今まで授業内で使った電子パーツや運営側が制作用に準備したパーツの使い方まとめ資料です。

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。


### LED赤、青: 
<img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)

<details><summary>使い方</summary>
1. obnizでの配線
<img src="https://i.gyazo.com/72603bdeeae78020b1a3625f06044b6d.png" alt="Image from Gyazo" width="500"/>

- LEDの長い脚をobnizの0番
- LEDの短い脚をobnizの1番

2. 使うノードとつなぎ方
- inject 2つ
- obniz function
- debug
<a href="https://gyazo.com/b685c59d9faa57a0a551037d0caa39e1"><img src="https://i.gyazo.com/b685c59d9faa57a0a551037d0caa39e1.png" alt="Image from Gyazo" width="500"/></a>


3. 各ノードの設定方法
- inject
1つ目: payloadの設定を「真偽」、trueにする
2つ目: payloadの設定を「真偽」、falseにする


- obniz functionのコード

```javascript
obniz.display.clear(); // 画面を消去

if (msg.payload === true) {
 // スイッチが押されている状態
 obniz.display.print('LED ON');
 obnizParts.led.on();
} else {
 // スイッチが押されていない状態
 obniz.display.print('LED OFF');
 obnizParts.led.off();
}


```


4. 初期化処理コードの編集

```javascript
obnizParts.led = obniz.wired('LED', { anode:0, cathode:1 });

```

5. 結果
injectのボタンtrueを押すと光り、falseを押すと消える。


■ 参考資料
[obnizの公式ドキュメント: LED](https://docs.obniz.com/ja/sdk/parts/LED/README.md)

</details>

---

### トランプ: 

<img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="50">, 出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino)
    <details><summary>使い方</summary>
    使い方
    </details>

---

### 温湿度センサ: 

<img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
    <details><summary>使い方</summary>
    使い方
    </details>

---

### 超音波距離センサー: 

<img src="https://akizukidenshi.com/img/goods/L/111009.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
    <details><summary>使い方</summary>
    使い方
    </details>



---


### 照度センサー(CdS): 

<img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
    <details><summary>使い方</summary>
    使い方
    </details>


---


### サーボモーター: 

<img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
    <details><summary>使い方</summary>
    使い方
    </details>



---


### ブザー: 

<img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="50">, 出典：[秋月電子通商](https://akizukidenshi.com/)
    <details><summary>使い方</summary>
    使い方
    </details>



---


### obnizのディスプレイ: 




---


### obnizのスイッチ: 





---
