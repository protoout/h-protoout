# 2. 外部サービス連携や情報取得をしてみよう② APIを使って情報取得


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


## NASAのAPIを使って、宇宙飛行士のジャーナルを取得してみる


### 1. 使うノード

- injectノード
- http requestノード: APIにこのデータください、とお願いするために使います。
- debug


[HTTPってなに？という方はこちらの記事を参照してください](../lesson06-iot-overview/03-network.md)


### 2. 手順

1. injectノード、http requestノード、debugノードを追加し図のようにつなぐ
<img src="https://i.gyazo.com/4cc9b58750f7f4864ab02a7faa1cb21f.png" alt="Image Description" width="500"/>


2. http requestノードを図のように設定する。APIキーは[こちらの資料](1G1lZX74bEyMyo9YwId6vUD_SVOj3IZyTHnGBUc8hsVs)の「NASA API」のキーを入力する。
<img src="https://i.gyazo.com/31f7db211f6a0b606c68772c4531ec75.png" alt="Image Description" width="500"/>


3. デプロイ後、injectノードのスイッチを押して、コンソールに結果が返ってくれば成功です。
<img src="https://i.gyazo.com/17a02c204783ee4adf59112b942f4be1.png" alt="Image Description" width="500"/>


## 2.お天気情報を取得するAPIを使ってみよう

今度は別のAPIを使ってみましょう。[Open Weather Map API](https://openweathermap.org/api)を使って、お天気の情報を取得します。

1. 


## 3. どんなAPIがあるか見て、どの様に使えそうか考えてみよう


- [今すぐ使える無料WebAPIまとめ](https://qiita.com/kazuki_tachikawa/items/7b2fead2a9698d1c15e8)

- [【随時更新】一風変わったWeb APIをまとめてみた](https://qiita.com/danishi/items/42d8adf6291515e62284)

- [API Hub](https://apidog.com/apihub/): いろいろなサードパーティのAPIがまとまっている

<a href="https://gyazo.com/4e9f8111e7da3ee740030da9a383774a"><img src="https://i.gyazo.com/4e9f8111e7da3ee740030da9a383774a.png" alt="Image from Gyazo" width="1372"/></a>




外部サービスを連携していくことで、業務効率化やに役立てることができます。

- お問い合わせメールが来たらその内容をTeamsに通知する
- オフィスのトイレの空き状況をTeamsに通知する



などなど、会社のレギュレーションも確認しながら、チャレンジしてみてくださいね。
　


---

**[◀ 目次ページに戻る](./readme.md)**
