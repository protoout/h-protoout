# マニュアル: マトリクスLED

8x8のマトリクスLEDです（`Keyestudio_HT16K33`）

<img src="https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/image.jpg" width="50">

> 出典：[obniz公式ライブラリ](https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/README.md)

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<details><summary>配線の仕方をクリックで開く</summary>
<img src="https://i.gyazo.com/13ab90f80705f099b43fdf75766033ed.png" alt="Image from Gyazo" width="500"/>

左から写真の向きで

- vcc: 0番ピン
- gnd: 1番ピン
- sda: 2番ピン
- scl: 3番ピン

</details>

## 2. 使うノードとつなぎ方

`Injectノード`と`obniz functionノード`を接続します。

## 3. 各ノードの設定方法

- obniz functionのコード

```javascript
const dots = [1,2,4,8,16,32,64,128]
matrix.dots(dots);
```

## 4. 初期化処理コードの編集

```javascript

obnizParts.matrix = obniz.wired("Keyestudio_HT16K33", { vcc:0, gnd:1, sda:2, scl:3 });

```

5. 結果

Injectノードを押すとマトリクスLEDが斜めに光ります。

<img src="https://i.gyazo.com/15da82b6277ebfdf68597b229ccaeb23.jpg" width="400px" />

■ 参考資料
[obnizの公式ドキュメント: マトリクスLED](https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/README.md)


## 6. 光らせ方を変える

function obnizの、`const dots = [1,2,4,8,16,32,64,128]`の配列を変更することで光らせ方を変更できます。

8x8のLEDマトリックスは、各行に8つのLEDを持つ、全体で64個のLEDを含むマトリックスです。各行のLEDの状態は、8ビットのバイナリ数値で表現されます。

1. LED Matrix Editorを使って、絵や文字をデザインしよう

[LED Matrix Editor](https://xantorohara.github.io/led-matrix-editor/)で表示したい絵や文字をデザイン。※ 赤一色のみ表示できます。

2. 右下の数字（16進数の数字）をコピー

<a href="https://gyazo.com/ddfe8039610713b5950bc8d4cb05db5c"><img src="https://i.gyazo.com/ddfe8039610713b5950bc8d4cb05db5c.png" alt="Image from Gyazo" width="500"/></a>

3. ChatGPTに、このマトリクスLED`Keyestudio_HT16K33`で読み込める形に変えてもらう

■ プロンプト

```
## system

あなたは8x8のマトリックスLEDのフォントメーカーです。

バイナリを10進数の配列に変更し下記のように出力します。

[0, 0, 28, 2, 30, 34, 30, 0]

 ## prompt

【ここに先ほどコピーした16進数の数字】

```

obniz functionノードの`const dots = `を出力されたものに書き換えてください。

<a href="https://gyazo.com/96198ece0adec09518ac5832f56e2fb0"><img src="https://i.gyazo.com/96198ece0adec09518ac5832f56e2fb0.png" alt="Image from Gyazo" width="500"/></a>


<details><summary>LEDマトリックスの基本 by ChatGPT</summary>
各行は1つの8ビット数値で表されます。
各ビットは1つのLEDの状態を示し、0はオフ、1はオンを意味します。
例えば、数値`255`はバイナリで`11111111`となり、8つのLEDがすべてオンになります。
具体例
1 = 00000001 （1行目の1番目のLEDがオン）
255 = 11111111 （2行目の全てのLEDがオン）
4 = 00000100 （3行目の3番目のLEDがオン）
dots 配列の各要素の意味
配列 const dots = [1, 255, 4, 8, 16, 32, 64, 128] の各要素は、それぞれの行のLEDの状態を示します。

例の解説:
1 はバイナリで 00000001。1行目の1番目のLEDがオン。
255 はバイナリで 11111111。2行目の全てのLEDがオン。
4 はバイナリで 00000100。3行目の3番目のLEDがオン。
8 はバイナリで 00001000。4行目の4番目のLEDがオン。
16 はバイナリで 00010000。5行目の5番目のLEDがオン。
32 はバイナリで 00100000。6行目の6番目のLEDがオン。
64 はバイナリで 01000000。7行目の7番目のLEDがオン。
128 はバイナリで 10000000。8行目の8番目のLEDがオン。
このように、配列 dots の各要素は各行のLEDの状態を8ビットのバイナリ数値で表しています。したがって、2行目を横一列にすべて光らせるには、その行のバイナリ表記を 11111111 とする必要があり、これは10進数で 255 となります。
</details>
