# 制作に役立つ道具

制作で役立つTipsやトラブルシューティング系のナレッジをまとめています。

## 1. よく使うもの

- [Node-REDの停止処理](https://qiita.com/n0bisuke/items/28d44edc290a0dddc8b0)
    - よく使います。
- [電子パーツマニュアル](./parts-manual/)
    - 今まで触れたものも含め今回用意しているパーツを使用する方法をまとめている資料です。

## 2. トラブルが起きたらみるところ

- [Node-REDで接続切ってるはずなのにプログラムが止まらない時](https://qiita.com/n0bisuke/items/ef82c303f98d62ae9cf4)
- [複数のサーバーでobnizが動いてしまっている時](https://qiita.com/n0bisuke/items/34c8389e371bd5d2f7f5)

## 3. Node-REDの開発ナレッジ

やりたいことがある...でも、どうやるの？ってときに見てください

### データの取扱系

- [functionノードの使い方: 基本的な使い方と生成AIにコードを書かせる方法](./function-node.md)
- [データの中から特定の数値のみ取り出して使うには？ changeノードを使ってJSONデータを扱う](./json-data.md)
- [取得した数値データを四捨五入したい: 計算処理いろいろ](./math-data.md)
- [取得したデータをテンプレートにはめ込んで表示したい: templateノードの使い方](../DAY1/dev_lesson/lesson02-node-red-basic/01_node-red-corenode.md#3-template%E3%83%8E%E3%83%BC%E3%83%89)

### フローの組み方系
- [取得したデータの値によって処理を分けたい: switchノードの使い方](../DAY1/dev_lesson/lesson02-node-red-basic/01_node-red-corenode.md#2-changeノードとswitchノード)

### コードの書き方系
- [検索して出てきたJavaScriptのコードをobnizノードで使えるように書き換えるには？](https://qiita.com/n0bisuke/items/ce783af305588664a6bc)
- [ノード内のコードを生成AIに書いてもらう方法]()
- [obnizで複数のパーツを同時に使いたい](./obniz-multiple-parts.md)

## 4. チュートリアルコンテンツ: 参考になりそうなサンプルで解説をします。
- [温湿度センサーと信号LEDを連動して熱中症アラートをつくる](./tutorials/01_temp_led.md)
- [CdSとサーボモーターを連動して明るさによってサーボモーターの角度を変える](./tutorials/02_servo_cds.md)
- [サーボモーターでピョコピョコ繰り返し処理](./tutorials/03_servo-pyokopyoko.md)

### Day2のハンズオンコンテンツ
- A. [OpenAIのノードをつかってみよう simple gtpノードでAPIから取得したデータを翻訳](/DAY2/dev_lesson/lesson03-handson/a_openai-node-gtp.md)
- B. [OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する](/DAY2/dev_lesson/lesson03-handson/a_openai-node-wisper.md)
- C. [Teachable Machineの利用](/DAY2/dev_lesson/lesson03-handson/c_teachable-machine.md)

## 5. 参考記事いろいろ

- [Node-RED から obniz ノードをつかってクリスマスソング＆キラキラ＆顔文字ダンスさせる！](https://qiita.com/tseigo/items/56c78be82b6276825ca6)
- [冷蔵庫の開けっ放し癖をobnizを使って無理やり直した](https://qiita.com/Yuki-Tamura-85/items/b4caf99e0f356a691b58)
- [もう電気を消し忘れません！](https://qiita.com/Ichiros_malt/items/bff24b1c964e854be9ec)

### 参考記事の調べ方

「obniz node-red ◯◯◯（パーツの名前）」を入力すると、参考記事を探しやすいです。

- [Qiita](https://qiita.com/): エンジニアに関する知識を記録・共有するためのサービスです。 プログラミングに関するTips、ノウハウ、メモを簡単に記録 & 公開することができます。

- [Zenn](https://zenn.dev/): Qiitaと同じくZennはエンジニアが技術・開発についての知見をシェアする場所です。


Node-REDでなく、JavaScriptの参考記事が出てきた場合はこの記事を参考にして書き換えてみてください。

- [検索して出てきたJavaScriptのコードをobnizノードで使えるように書き換えるには？](https://qiita.com/n0bisuke/items/ce783af305588664a6bc)
