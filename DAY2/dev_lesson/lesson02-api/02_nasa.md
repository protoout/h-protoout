# 2. 外部サービス連携や情報取得をしてみよう② APIを使って情報取得


■ APIとは？
API（アプリケーション・プログラミング・インターフェース）は色々な外部サービスを連携してデータの取得や連携などを行う仕組みのことです。通常HTTPプロトコルを用いて、データの送受信が行われます。



具体的には、

- 天気情報
- 株価の変動
- 商品名や詳細情報

こういった情報を取得することや、

- LINEで生成AIを使ったBotを自作する
- Stripe決済を使って自分のアプリに決済機能を組み込む


外部サービスの一部の機能を使うことで独自のサービスを作ることもできます。



APIを活用すれば、まったくのゼロからすべての機能を構築必要はありません。



ここでは、簡単に公開されているAPIを使う体験をしてみましょう。


## NASAのAPIを使って、NASAのジャーナルを取得してみる

[NASA APIs](https://api.nasa.gov/): NASAが公開しているAPIです。毎日異なる画像や写真、専門の天文学者によって書かれた文章で、宇宙の魅力を発信するAPIから、画像と文章を取得してみます。


### 1. 使うノード

- injectノード
- http requestノード: APIにこのデータください、とお願いするために使います。
- debug


[HTTPってなに？という方はこちらの記事を参照してください](/tools/column/iot-overview/03-network.md)


### 2. 手順

1. injectノード、http requestノード、debugノードを追加し図のようにつなぐ
<img src="https://i.gyazo.com/4cc9b58750f7f4864ab02a7faa1cb21f.png" alt="Image Description" width="500"/>


2. http requestノードを図のように設定する。APIキーは[こちらの資料](https://docs.google.com/spreadsheets/d/1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs/edit#gid=0)の「NASA API」のキーを入力する。

<a href="https://gyazo.com/1f90fcbed097ca05cc868615b9b363ff"><img src="https://i.gyazo.com/1f90fcbed097ca05cc868615b9b363ff.png" alt="Image from Gyazo" width="524"/></a>

- メソッド: GET
- 出力方式: JSONオブジェクト

URLには下記の【API KEY】を書き換えて入力してください。※「【】」は不要です。

また、スペースなど余計な文字は入れないでください。

```
https://api.nasa.gov/planetary/apod?api_key=【API KEY】

```



3. デプロイ後、injectノードのスイッチを押して、コンソールに結果が返ってくれば成功です。
<img src="https://i.gyazo.com/17a02c204783ee4adf59112b942f4be1.png" alt="Image Description" width="500"/>


返ってきたデータの「url」とかいてあるところにあるURLは、宇宙の画像です。URLをコピーしてブラウザからアクセスしてみましょう。
<a href="https://gyazo.com/2fbb69ee50e6e948e7cc50c0844e5569"><img src="https://i.gyazo.com/2fbb69ee50e6e948e7cc50c0844e5569.png" alt="Image from Gyazo" width="285"/></a>

<img src="https://apod.nasa.gov/apod/image/2405/NGC2169LRGBQHY183HR_c1024.jpg" width="300">


### 3. 時間がある人向け: 取得したデータをWebページに表示したい！

せっかく取得したデータ、ブラウザでWebページとして表示してみたいですよね。

先ほど取得したデータを、ウェブページとして表示する方法を説明します。



1. ノードの配置と接続

さきほど作ったものに3つのノードを追加します。

- http in: 外部からアクセスできる場所をつくる。このノードを置くと、ウェブページのURLができあがるようなイメージ。
- template: ウェブサイトに表示する内容をここに書く
- http responce: ブラウザにWebページの情報を返す。これにより、ブラウザから表示できるようになる

<a href="https://gyazo.com/ab234703ff567b71815d32360fac84e0"><img src="https://i.gyazo.com/ab234703ff567b71815d32360fac84e0.gif" alt="Image from Gyazo" width="600"/></a>


2. ノードの設定

- http in

アクセスするURLをhttp inで設定します。

URLに`/nasa`と入れます。（「nasa」部分は任意の英数字でOKです。）

この設定により、ウェブページのURLは下記のようになります。

`http://【みなさんのNode-RED URL（URLバーに表示されている部分）】:1880/nasa`


※ enebularの場合は右上「i」にカーソルをあてると出てくるのがWebページのURLです。
<a href="https://gyazo.com/71ad81be655748046be291d43bc2d881"><img src="https://i.gyazo.com/71ad81be655748046be291d43bc2d881.png" alt="Image from Gyazo" width="352"/></a>

`https://xxxxxxxxx.herokuapp.com/nasa`

となります。


<a href="https://gyazo.com/070c36c4dbc7777a99a9d6e5bf74566e"><img src="https://i.gyazo.com/070c36c4dbc7777a99a9d6e5bf74566e.gif" alt="Image from Gyazo" width="600"/></a>

- template

ここではウェブサイト構築でよく使われる、HTMLというマークアップ言語を使います。


<a href="https://gyazo.com/ca05b240145bb462dd01eafb252935e1"><img src="https://i.gyazo.com/ca05b240145bb462dd01eafb252935e1.gif" alt="Image from Gyazo" width="600"/></a>

```html

<html>
<head>
    <title>H24 NASA APIテスト</title> <!--タイトル-->
</head>
<body>
    
<h1>NASA</h1><!--見出し1-->
<img src="{{payload.url}}" width="500"> <!--画像として、APIから取得したURLを表示する-->
<p>
{{payload.explanation}}  <!--APIから取得したテキスト情報を表示する-->
</p>
    
</body>
</html>

```



自分で作るときは、生成AIに書いてもらいましょう！

プロンプトのサンプル

```
## システム
要件に沿ってHTMLをかいてください。
CSSはHTML内に記述し一つにおさめてください。

## 出力のサンプル
<head>
    <title>H24 NASA APIテスト</title> <!--タイトル-->
</head>
<body>
    
<h1>NASA</h1><!--見出し1-->
<img src="{{payload.url}}" width="500"> <!--画像として、APIから取得したURLを表示する-->
<p>
{{payload.explanation}}  <!--APIから取得したテキスト情報を表示する-->
</p>
    
</body>
</html>

## 要件

- テキストと画像を横に3つ並べる
- テキストの内容と画像のURLは以下の通り
1. {{payload.text1}}{{payload.img1}}
2. {{payload.text2}}{{payload.img1}}
3. {{payload.text3}}{{payload.img1}}

```

サンプルを試すと、下記のように表示できるHTMLが生成されました。
<a href="https://gyazo.com/3484e70918b921a9041f364082a9bd16"><img src="https://i.gyazo.com/3484e70918b921a9041f364082a9bd16.jpg" alt="Image from Gyazo" width="500"/></a>


3. アクセスしてみましょう

URLにアクセスして、ウェブページが表示されれば成功です！

`http://【みなさんのNode-RED URL】:1880/nasa`

<a href="https://gyazo.com/379c58837293cbca3538ff38810653ce"><img src="https://i.gyazo.com/379c58837293cbca3538ff38810653ce.jpg" alt="Image from Gyazo" width="500"/></a>



### 完成したフロー

```json
[{"id":"45edf3530a1ccca6","type":"inject","z":"71b6251b827a5d40","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":240,"y":200,"wires":[["c7fc2eaae4424f10"]]},{"id":"c7fc2eaae4424f10","type":"http request","z":"71b6251b827a5d40","name":"","method":"GET","ret":"obj","paytoqs":"ignore","url":"https://api.nasa.gov/planetary/apod?api_key=【APIキー】","tls":"","persist":false,"proxy":"","insecureHTTPParser":false,"authType":"","senderr":false,"headers":[],"x":430,"y":260,"wires":[["9d1ecf939443eef7","488a55c54d99765c"]]},{"id":"9d1ecf939443eef7","type":"debug","z":"71b6251b827a5d40","name":"debug 19","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":620,"y":200,"wires":[]},{"id":"e312dcbee02b1a8f","type":"http in","z":"71b6251b827a5d40","name":"","url":"/nasa","method":"get","upload":false,"swaggerDoc":"","x":240,"y":320,"wires":[["c7fc2eaae4424f10"]]},{"id":"6e9bb0226855ebab","type":"http response","z":"71b6251b827a5d40","name":"","statusCode":"","headers":{},"x":790,"y":320,"wires":[]},{"id":"488a55c54d99765c","type":"template","z":"71b6251b827a5d40","name":"","field":"payload","fieldType":"msg","format":"html","syntax":"mustache","template":"<html>\n\n<head>\n    <title>H24 NASA APIテスト</title>\n</head>\n\n<body>\n\n    <h1>NASA</h1>\n    <img src=\"{{payload.url}}\" width=\"500\">\n    <p>\n        {{payload.explanation}}\n    </p>\n\n</body>\n\n</html>","output":"str","x":620,"y":320,"wires":[["6e9bb0226855ebab"]]}]

```



## 2. どんなAPIがあるか見て、どの様に使えそうか考えてみよう

今回は簡単にすぐ使えるNASAのAPIを選んで情報を取得しました。


LINE、Google系サービス、Amazon、楽天...


普段、仕事やプライベートで使っている有名なサービスの多くは、APIを提供しています。



外部サービスを連携していくことで、業務効率化にも役立てることができます。

- お問い合わせメールが来たらその内容をTeamsに通知する
- オフィスのトイレの空き状況をTeamsに通知する


などなど、会社のレギュレーションも確認しながら、チャレンジしてみてくださいね。


どのようなAPIがあるのか、眺めてみましょう！


- [今すぐ使える無料WebAPIまとめ](https://qiita.com/kazuki_tachikawa/items/7b2fead2a9698d1c15e8)

- [【随時更新】一風変わったWeb APIをまとめてみた](https://qiita.com/danishi/items/42d8adf6291515e62284)

- [API Hub](https://apidog.com/apihub/): いろいろなサードパーティのAPIがまとまっている

<a href="https://gyazo.com/4e9f8111e7da3ee740030da9a383774a"><img src="https://i.gyazo.com/4e9f8111e7da3ee740030da9a383774a.png" alt="Image from Gyazo" width="1372"/></a>





---

**[◀ 目次ページに戻る]( ../readme.md)**