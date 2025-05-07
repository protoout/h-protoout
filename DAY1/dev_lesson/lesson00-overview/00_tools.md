# この授業で使うツール

## 1.使用するモノ（デバイス、センサー、アクチュエーターなど）

下記が揃っているか確認をしてください。

| 名称 | 画像 | 説明 | URL |
| --- | --- | ----------- | --- |
|obniz Board <br> または <br> obniz Board 1Y　| <img src="https://akizukidenshi.com/img/goods/L/114930.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/) | 制御の中心となるマイコンボードです。[^1]| https://akizukidenshi.com/catalog/g/g113685/ <br> https://akizukidenshi.com/catalog/g/g114930/ |
|ブレッドボード（BB-601）| <img src="https://akizukidenshi.com/img/goods/L/105155.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 電子部品をはんだ付けせずに配線するために使います | https://akizukidenshi.com/catalog/g/g105155/ |
|ジャンパワイヤー| <img src="https://akizukidenshi.com/img/goods/L/105371.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | ブレッドボードとセットで配線のために使います | https://akizukidenshi.com/catalog/g/g115869/ <br> https://akizukidenshi.com/catalog/g/g105159/ |
|給電用USBケーブル <br> TypeA->microB <br> または <br> TypeA->TypeC| <img src="https://akizukidenshi.com/img/goods/L/117017.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/) | obniz Board の給電用ケーブルです。 | https://akizukidenshi.com/catalog/g/g117016/ <br> https://akizukidenshi.com/catalog/g/g117017/ <br>（実物と異なる場合があります。）|
|給電用USBアダプタ| <img src="https://akizukidenshi.com/img/goods/L/117092.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)   |  obniz Boardの給電用です。二人1組の場合と単独の物が両方あります。 | https://akizukidenshi.com/catalog/g/g117092/ <br>（実物と異なる場合があります。） |
|LED赤、青(OSR6LU5B64A-5V,OSB5SA5B64A-5V)| <img src="https://akizukidenshi.com/img/goods/L/112519.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 発光ダイオードです。電気を流すと光ります。赤と青の2種類があります。 | https://akizukidenshi.com/catalog/g/g112517/ <br> https://akizukidenshi.com/catalog/g/g112519/ |
|パトランプ（KS0310）| <img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="150"><br>出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino) | 信号機のように赤、黄、緑のLEDが一つのモジュールになっています。 | https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino |
|サーボモーター（SG-90）| <img src="https://akizukidenshi.com/img/goods/L/108761.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 指定した角度に回転する小型のモーターです。ロボットのアームなどに使用されます。 | https://akizukidenshi.com/catalog/g/g108761/ |
|ブザー（PKM13EPYH4000-A0）| <img src="https://akizukidenshi.com/img/goods/L/104118.jpg" width="150"> <br>出典：[秋月電子通商](https://akizukidenshi.com/) | 電気信号を音に変換するスピーカーです。アラームやメロディーを鳴らすのに使います。 | https://akizukidenshi.com/catalog/g/g104118/ |
|超音波距離センサー（HC-SR04）| <img src="https://akizukidenshi.com/img/goods/L/111009.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 超音波を発射し、反射して戻ってくる時間から距離を測定するセンサーです。 | https://akizukidenshi.com/catalog/g/g111009/ |
|照度センサー(CdSセル, MI527/MI5527)| <img src="https://akizukidenshi.com/img/goods/L/100110.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 明るさを検知するセンサーです。光の強さによって抵抗値が変化します。 | https://akizukidenshi.com/catalog/g/g100110/ |
|カーボン抵抗（CFS50J330RB）| <img src="https://akizukidenshi.com/img/goods/L/107812.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 電流の流れを制限する部品です。LEDなどと組み合わせて使用します。 | https://akizukidenshi.com/catalog/g/g107812/ |
|温湿度センサ（DHT20）| <img src="https://akizukidenshi.com/img/goods/L/116732.jpg" width="150"><br>出典：[秋月電子通商](https://akizukidenshi.com/)  | 周囲の温度と湿度を計測できるセンサーです。気象観測などに使用します。 | https://akizukidenshi.com/catalog/g/g116732/ |


> [!WARNING]
> **使う場所に注意！**  
> obniz Board はノートパソコンの上に置かず、机の上など電気を通さない場所に置きましょう。
   
---- 
  
## 2.使用するアプリケーション
  
1. GitHub: この授業資料です。基本的にこの資料を手元で見ながら進めていただきます。また、授業中TAに質問したい事項を投稿いただきます。
2. Effibot: AI アシスタントです。実装の際に活用します。後ほど練習します。
3. Miro: ホワイトボードツール。アイデア出しや整理で使用します。
4. SharePoint: 最終アイデアを記事としてまとめ、投稿する場所です。
  
1日目は、1 ~ 3 を使います。   
  
> [!IMPORTANT]
> **何か足りないものがあれば、手を挙げて講師陣にお知らせください。**   

---

**[◀ 目次ページに戻る](../readme.md)**

[^1]: [マイコンとは？](https://edn.itmedia.co.jp/edn/articles/2408/20/news027.html)
