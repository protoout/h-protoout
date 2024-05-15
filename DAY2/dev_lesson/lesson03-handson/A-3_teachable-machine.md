# A-3. ハンズオン: Teachable Machineで独自モデルの作成と画像判定

※このハンズオンはSSL（HTTPS）環境じゃないと後半が進めません。

Teachable MachineはGoogleが公開している機械学習を楽しく使えるノーコードツールです。

> こんな判定がライトに出来てだいぶ楽しい⭐️。
> 
> [<img src="https://i.gyazo.com/456af186a95b5cf057f451e55f003fdf.png" width="400px" />](https://twitter.com/n0bisuke/status/1789617932407808302)

## Teachable Machine

「これはコップです、これは人です。」など汎用的な画像認識はGooeleやOpenAIなど巨人たちが頑張って作ってくれてますが、

**「これは"秋葉原のカムイというお店のカレー"です、ボンディのカレーです」**

などニッチな情報を判定したいときに適切なモデルはありません。

自分自身の仕事ややりたいことに近づけば近づくほど、適切なモデルが無く、自分でモデルを作るということを世の中の人たちは研究していたりします。
（GPT-4oが出て、モデル作る必要あるかねぇという会話も聞こえてきています。世界が変わった。。。）

今までモデルを作るのが大変で専門的な知識が必要でしたがTeachable Machineを使うと簡単にモデルを作ることが出来ます。

> https://teachablemachine.withgoogle.com/
> 
> <img src="https://i.gyazo.com/fbe12966243dc8fae848c9500b807213.png" width="400px" />

## 1. Teachable Machineのモデル作成

### 1-1. Teachable Machineのモデル作成画面まで

指示に沿って進んでみましょう。

- 「Get Started（使ってみる）」をクリック

> <img src="https://i.gyazo.com/4aa6aa6236a2b6af6595f143cdf5fe68.png" width="400px" />

- 画像プロジェクトを選択します。

> <img src="https://i.gyazo.com/3102e9b541cad46c885439ddee701963.jpg" width="400px" />

- 標準の画像モデルを選択します。

> <img src="https://i.gyazo.com/4fdfb10b7ad728fea7a7d6a9b4a31db7.png" width="400px" />

- このような画面まで来たら準備OKです。

> <img src="https://i.gyazo.com/44df8918fdc71441fea086a9fe087dd5.png" width="400px" />

### 2. Teachable Machineのモデル作成

以下のGIF画像のように操作してみましょう。

ジャンケン判定のモデルを作っています。

- Webカメラを使って画像を撮り、学習させてモデルを作成します。
- 作成されたモデルを使うことでジャンケンの判定が出来ます。

> <img src="https://i.gyazo.com/cca0635b76e38b1a9b928bc3d3703660.gif" width="400px" />

また、`Class 1`などのラベルには`グー`や`チョキ`など文字を入れてみましょう。

> 画像で学習させるのであらゆるモデルを作れます。本の裏表を判定するモデルを作っている例です。
> 
> <img src="https://i.gyazo.com/066211c5b882751825de81158753449b.png" width="400px" />

### 3. モデルをエクスポート

モデルが出来たらモデルをエクスポートします。一時的に画像を含んだデータがアップロードされますが、プライバシーに配慮してすぐに消され、抽出したデータのみがGoogleのサーバーに保存される模様です。

> <img src="https://i.gyazo.com/28635275adee5bbff80f03ae81e9da3f.png" width="400px" />

> <img src="https://i.gyazo.com/ff856fcc7813abe7278f6f30b591ccbd.png" width="400px" />

完了すると共有可能なリンクが生成されます。

> 例: https://teachablemachine.withgoogle.com/models/TzKrAzfpN/ (のびすけジャンケンモデル)

ここまで出来たら前半終了です。

## 2. 作成したモデルを使ってNode-REDに組み込む

作成したモデルを使ってNode-RED連携をしてみましょう。

### 2-1. Node-REDに利用するノードのインストール

まずは必要な素材をインストールしてください。

- `node-red-contrib-teachable-machine`
    - teachable-machineで作成したモデルを使用するためのノード このノードは「image Project」のみに対応しているようです。
    - https://flows.nodered.org/node/node-red-contrib-teachable-machine

↓以下の2つは既にインストールされていると思われますが、もしまだでしたらインストールしてください。

- `node-red-contrib-browser-utils`
    - カメラを使えるようになります。
    - https://flows.nodered.org/node/node-red-contrib-browser-utils
- `node-red-contrib-image-output`
    - 撮影した画像のプレビューができるようになります。
    - https://flows.nodered.org/node/node-red-contrib-image-output


> <img src="https://i.gyazo.com/f3d3f76405b85e266165ae625f4a99a4.gif" width="400px" />

> <img src="https://i.gyazo.com/04000b3380bb4ee0ac59e58d3ae6a827.png" width="400px" />

## 他の技術とTeachable Machineを組み合わせた例

プロトアウトスタジオの受講生の記事抜粋です。

- LINE Bot
  - [憧れのギニュー特戦隊の誰に似てるか判定するLINEbotを作ったから、ぜってぇ見てくれよなっ！ - Qiita](https://qiita.com/Teru_3/items/109517e6a6e3b761285d)
  - [現役、理学療法士が姿勢の画像を送るとその姿勢について教えてくれるLINE botを作った - Qiita](https://qiita.com/yusei2629/items/da07d877a98c94abb3c9)
- obniz
  - [画像から機械学習したモデルで、酔っ払っているかどうかを判断してアウトだったら警報色ライトをつけた - Qiita](https://qiita.com/Sugizo50073508/items/c34df866fb46276d6ade)
