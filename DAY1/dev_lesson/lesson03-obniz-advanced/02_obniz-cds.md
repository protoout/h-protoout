# 2. 照度センサー（CdS）

### 2-0 そもそもセンサーとはなにか？

環境の変化（明るさ、圧力、温度etc...）を検出し、他のシステムに出力するデバイスです。

物理現象をアナログ電圧や場合によってはデジタル信号に変換します。



![2019-06-20_19h27_25_result.jpg (441.4 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/07ce0f24-6b93-47ed-b668-9153aae9769d.jpg)

CdSといい、センサー部分にあたる光の強さによって抵抗値が変化します。  
（**可変抵抗素子**といいます）

通常の抵抗器（**固定抵抗素子**）と組み合わせることで、この「抵抗値の変化」を「電圧値の変化」として取り出すことができます。
このセンサーはobnizのドキュメントにはありませんが、電子部品の発展編として実際に扱ってみます。




### 2-1. obnizとの接続

![2019-06-20_19h27_30_result.jpg (408.9 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/909d0f27-cd78-4386-9c6a-913114b1ae4b.jpg)

- CdS:1個
- 抵抗330Ω:1個
- ブレッドボード:1個
- ジャンパワイヤー赤:1本
- ジャンパワイヤー黒:1本
- ジャンパワイヤー白:1本

以上の6点の部品を準備してください。

[![Image from Gyazo](https://i.gyazo.com/aea0f2684723de82e05699203291fb76.png)](https://gyazo.com/aea0f2684723de82e05699203291fb76)

> 抵抗の数値は、カラーコードという色の帯で表現されています。
> 330Ωは `橙橙茶金` となります。  
> このあたりは[抵抗値早見表](http://part.freelab.jp/s_regi_list.html)などを参考にしてみてください。

(🚨：火傷の危険があります。注意レベルを上げましょう。)  
下記の回路をよく見て、接続を間違えないようにしましょう。

> CdSセルや抵抗が**含まれない**回路（ショート、短絡とも言います）があると、大量の電流が流れ高温になり、ブレッドボードが溶けたり、火傷の恐れがあります。

![2019-06-20_19h27_51_result.jpg (183.6 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/71cb5fbc-3f61-47e3-aaef-9da67ccc290e.jpg)

![2019-06-20_19h27_46_result.jpg (307.1 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/cbd3510a-9c8f-47eb-84c8-b99edb9c8336.jpg)

まずブレッドボードを横向き（横長方向）にし、CdSと抵抗を配置します。  
極性はありませんので方向は気にしなくてよいです。


図と同じ様に接続した場合、
明るくなると抵抗値が低くなる（電気が通りやすい）→ 高めの値が出ます
暗くなると抵抗値が高くなる（電気が通りにくい） → 低めの値が出ます


<details>
<summary>どうして抵抗器をつなぐ必要があるのか？「分圧」について</summary>

電圧は高い方から低い方に流れます。

図
同じ抵抗値の抵抗が2つついていると、真ん中の電圧は2.5Vとなります。

図
抵抗値が異なる抵抗が2つあると、抵抗値の比率に応じた電圧の値となります。

これを分圧といいます。

図
適切な抵抗値の抵抗器を接続することで、CdSセルから明るさに応じた値を取得することができるようになります。

図
抵抗器をつけずにCdSセルをつなげると、値は0Vになってしまいます。つまり、明るさの値を取ることができません。

</details>


次にジャンパワイヤ3本を写真のようにブレッドボードに挿し、さらに以下の通りにobnizと接続します。

- obniz 0 - ジャンパワイヤ赤
- obniz 1 - ジャンパワイヤ白
- obniz 2 - ジャンパワイヤ黒

![2019-06-20_19h27_58_result.jpg (298.9 kB)](https://img.esa.io/uploads/production/attachments/3062/2019/06/20/8131/1b53f227-13cb-4f93-86bc-26d7673c834c.jpg)

### 2-2. 仕組み

[![Image from Gyazo](https://i.gyazo.com/d8f564c5f77f0608a31384faae4f9781.jpg)](https://gyazo.com/d8f564c5f77f0608a31384faae4f9781)

obnizの端子の機能を以下のように設定し、このうち1番端子の「電圧」を計測します。

- obniz 0 - 電圧出力（5V）
- obniz 1 - 電圧入力（CdSと抵抗の**分圧**）
- obniz 2 - 電圧出力（0V）

### 2-3. Node.jsで動かす

`07_cds.js`というファイルを新規作成し、以下のソースコードを動かしてみましょう。

```js:07_cds.js
const Obniz = require('obniz');
const obniz = new Obniz('obnizのデバイスID');

obniz.onconnect = async () => {
  obniz.io0.output(true);  // io0電圧を5Vに（電源＋）
  obniz.io2.output(false); // io2電圧を0Vに（電源−）

  // io1をアナログピンに(センサーの値を取得)
  obniz.ad1.start((voltage) => {
    // センサーの値が変わるたびに実行される
    console.log(`changed to ${voltage} v`);
  });
}
```

[![Image from Gyazo](https://i.gyazo.com/bd601bf2e7ad760a85064af9dc6ced4f.gif)](https://gyazo.com/bd601bf2e7ad760a85064af9dc6ced4f)

ここで使っている関数はCdS専用のものではなく、端子にかかっている電圧を測定して数値で表現できるような、汎用的なものとなります。  
obnizドキュメントにおいては  
[AD - obniz Docs](https://obniz.com/ja/doc/reference/common/ad)  
がこの関数に対応したページとなります。

> 参考：[obnizとNode.jsでCdSセル(照度センサ)を使ってみる](https://zenn.dev/protoout/articles/01-obniz-nodejs-cds)

---

その他、obnizで公式に動作確認・サポートされているパーツは、[obnizパーツライブラリ](https://docs.obniz.com/ja/sdk/parts)から参照できます。

この中にないものを触ってみたい場合も動かせる可能性はありますが、まずはパーツライブラリから選ぶのが手っ取り早くてオススメです。