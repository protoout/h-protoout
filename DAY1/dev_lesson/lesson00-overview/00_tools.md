# この授業の進め方と使うツール

## 1.使用するモノ（デバイス）

下記が揃っているか確認をしてください。
| 名称 | 画像 | 説明 |
| --- | --- | ----------- |
|obniz Board 1Y（obniz009）| <img src="https://akizukidenshi.com/img/goods/L/114930.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/) |マイコン。もしくは obniz Board(obniz001) を使います|
|ブレッドボード（BB-601）| <img src="https://akizukidenshi.com/img/goods/L/105155.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 電子部品をはんだ付けせずに配線するために使います |
|ジャンパワイヤー（BBJ-20）| <img src="https://akizukidenshi.com/img/goods/L/105371.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | ブレッドボードとセットで配線のために使います |
|給電用USBケーブル A->C| <img src="https://akizukidenshi.com/img/goods/L/117017.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/) | obniz Board の給電をします           |
|給電用USBアダプタ| <img src="https://akizukidenshi.com/img/goods/L/117092.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)   |  obniz Board の給電をします           |
|LED赤、青(OSR6LU5B64A-5V,OSB5SA5B64A-5V)| <img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|パトランプ（KS0310）| <img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="150"><br>出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino) |             |
|温湿度センサ（DHT20）| <img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|カーボン抵抗（CFS50J330RB）| <img src="https://akizukidenshi.com/img/goods/L/107812.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|超音波距離センサー（HC-SR04）| <img src="https://akizukidenshi.com/img/goods/L/111009.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|照度センサー(CdSセル, MI527/MI5527)| <img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|サーボモーター（SG-90）| <img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  |             |
|ブザー（PKM13EPYH4000-A0）| <img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="150"> <br>出典：[秋月電子通商](https://akizukidenshi.com/) |             |

## 2.使用するアプリケーション

1. GitHub: この授業資料。基本的にこの資料を手元で見ながら進めていただきます。
2. Effibot: 生成AIを使いながら実装を行います。
3. [Miro](https://miro.com/app/board/uXjVKPW27-k=/): ホワイトボードツール。授業中に出てきた疑問や質問、アイデア出しで使用。
4. [SharePoint](https://hitachigroup.sharepoint.com/sites/syagai_jyujyu/S000182/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2Fsyagai%5Fjyujyu%2FS000182%2FShared%20Documents%2F%E3%83%86%E3%82%B9%E3%83%88&viewid=ca370411%2D8eb9%2D45cf%2D9724%2D7bfbbed13b54): 最終アイデアを記事としてまとめ、投稿する場所。

1日目は、1と2をつねに開いておいてください。


### 練習: Miroにチーム名を書いてみよう！
[Miro](https://miro.com/app/board/uXjVKPW27-k=/)にアクセスし、チーム名を決めて書いてみましょう！  

## 3.進め方
1. 説明: これから何をやるか、みなさんに何をしていただきたいか、基本的な説明をします
2. ハンズオン: 資料の通りに手を動かす
3. 演習: 考えて作ってみる


#### 1. わからない、うまくいかない事があるときは？

TAが助けにいきます！Miroにある自分たちのテーブルに**ピンクの付箋**で疑問を書いてください。

解決したら、**付箋の色をブルーに変更** してください。


#### 2. 画像が小さくて見えない！
<a href="https://gyazo.com/1f91a73b903896741c8c1f11ac5734a3"><img src="https://i.gyazo.com/1f91a73b903896741c8c1f11ac5734a3.png" alt="Image from Gyazo" width="100"/></a>


画像が小さかったら、別タブで表示して各自で拡大表示してくださいね。
クリックすると大きく開きます。


#### 3. 授業のスピードが自分にとってゆっくりに感じるとき

各トピック早く進められる人は他の人を待たずに資料をみて先に進めても大丈夫です。

それぞれの演習には、簡単にできるものと少しひねった応用編を用意しています。

速く進めて、演習の応用に取り組むのもOKです！




**1ページ終わるごとに、目次ページに戻りましょう。**

すべての授業資料の最下部に、目次のリンクがあります。


---

**[◀ 目次ページに戻る](../readme.md)**
