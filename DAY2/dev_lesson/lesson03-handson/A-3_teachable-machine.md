# A-3. ハンズオン: Teachable Machine で独自モデルの作成と画像判定

※このハンズオンは SSL（HTTPS）環境じゃないと後半が進めません。

Teachable Machine は Google が公開している機械学習を楽しく使えるノーコードツールです。

> こんな判定がライトに出来てだいぶ楽しい⭐️。
> 
> [<img src="https://i.gyazo.com/456af186a95b5cf057f451e55f003fdf.png" width="400px" />](https://twitter.com/n0bisuke/status/1789617932407808302)

## Teachable Machine

「これはコップです、これは人です。」など汎用的な画像認識は Gooele や OpenAI など巨人たちが頑張って作ってくれてますが、

**「これは"秋葉原のカムイというお店のカレー"です、ボンディのカレーです」**

などニッチな情報を判定したいときに適切なモデルはありません。

自分自身の仕事ややりたいことに近づけば近づくほど、適切なモデルが無く、自分でモデルを作るということを世の中の人たちは研究していたりします。

今までモデルを作るのが大変で専門的な知識が必要でしたが Teachable Machine を使うと簡単にモデルを作ることが出来ます。

> https://teachablemachine.withgoogle.com/
> 
> <img src="https://i.gyazo.com/fbe12966243dc8fae848c9500b807213.png" width="400px" />

## 1. Teachable Machine のモデル作成

### 1-1. Teachable Machine のモデル作成画面まで

指示に沿って進んでみましょう。

- 「Get Started（使ってみる）」をクリック

> <img src="https://i.gyazo.com/4aa6aa6236a2b6af6595f143cdf5fe68.png" width="400px" />

- 画像プロジェクトを選択します。

> <img src="https://i.gyazo.com/3102e9b541cad46c885439ddee701963.jpg" width="400px" />

- 標準の画像モデルを選択します。

> <img src="https://i.gyazo.com/4fdfb10b7ad728fea7a7d6a9b4a31db7.png" width="400px" />

- このような画面まで来たら準備OKです。

> <img src="https://i.gyazo.com/44df8918fdc71441fea086a9fe087dd5.png" width="400px" />

### 1-2. Teachable Machine のモデル作成

以下の gif 画像のように操作してみましょう。

ジャンケン判定のモデルを作っています。

- Web カメラを使って画像を撮り、学習させてモデルを作成します。
- 作成されたモデルを使うことでジャンケンの判定が出来ます。

> <img src="https://i.gyazo.com/cca0635b76e38b1a9b928bc3d3703660.gif" width="400px" />

また、`Class 1`などのラベルには`グー`や`チョキ`など文字を入れてみましょう。

> 画像で学習させるのであらゆるモデルを作れます。本の裏表を判定するモデルを作っている例です。
> 
> <img src="https://i.gyazo.com/066211c5b882751825de81158753449b.png" width="400px" />

### 1-3. モデルをエクスポート

モデルが出来たらモデルをエクスポートします。一時的に画像を含んだデータがアップロードされますが、プライバシーに配慮してすぐに消され、抽出したデータのみがGoogleのサーバーに保存される模様です。

> <img src="https://i.gyazo.com/28635275adee5bbff80f03ae81e9da3f.png" width="400px" />

> <img src="https://i.gyazo.com/ff856fcc7813abe7278f6f30b591ccbd.png" width="400px" />

完了すると共有可能なリンクが生成されます。

> 例: https://teachablemachine.withgoogle.com/models/TzKrAzfpN/ (のびすけジャンケンモデル)

ここまで出来たら前半終了です。

## 2. 作成したモデルを使ってNode-REDに組み込む

作成したモデルを使って Node-RED 連携をしてみましょう。

### 2-1. Node-RED に利用するノードのインストール

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

このような操作でインストールできます。

> <img src="https://i.gyazo.com/f3d3f76405b85e266165ae625f4a99a4.gif" width="400px" />

上手くいくと左のサイドバーにオレンジ色の`Teachable Machineノード`が追加されます。

> <img src="https://i.gyazo.com/04000b3380bb4ee0ac59e58d3ae6a827.png" width="400px" />

### 2-2. 設定など

- 配線

まずは、ノードを設置して繋げます。写真のようにノードを配置してみましょう。

> `Cameraノード`, `Teachable Machineノード`, `Image Previewノード`, `Switchノード`, `Debugノード`
>
> <img src="https://i.gyazo.com/b9c5eb1c1a52ea2dcc65bbb63fd47b3d.png" width="400px" />

- `Teachable Machineノード`の設定

`Teachable Machineノード`の設定のURLに先ほど自身が学習したモデルのURLを入れて保存します。

> 例: https://teachablemachine.withgoogle.com/models/YzQquwL7M/ （太陽拳と気功法の判定）
> 
> <img src="https://i.gyazo.com/6a407f929ea056989fa1a853d0fcc8f4.png" width="400px" />

- Switchノードで条件分岐

プロパティのプルダウンを`msg`にして`payload[0].class`と入れます。（ちょっと難しいかも）

あとは条件式にTeachable Machineで設定していたクラス名を設定します。`Class 1`や`Class 2`という文字列のまま学習させた人は`Class 1`などのテキストを入れましょう。

> <img src="https://i.gyazo.com/8f1fb0c258a9fb804c7f76c81805ac57.png" width="400px" />

最後にデプロイして完成です。

### 2-3. 使ってみる

`Cameraノード`のボタンをクリックするとPCのカメラで撮影がされます。（最初だけ許可を求められると思うので許可しましょう。）

デバッグノードに結果が表示されるはずです。

> <img src="https://i.gyazo.com/b9b58efa323389388527845029b56756.png" width="400px" />

お疲れ様でした。

## 3. 応用を考えてみる

これで条件分岐もできるので、例えば

- 入館証などを学習させておいて特定の入館証だったら処理を行う
- 魚の写真を学習させておいて鮮度が良ければ処理を行う

など出来そうです。

また、処理を行った先にTeamsに通知をしたり、obnizでサーボを回したりと接続することも可能なので色々な入力や判定の起点に使えそうですね。

> こんな感じの接続もできます。
> 
> <img src="https://i.gyazo.com/cd887f784de9df5224e7ae6e84313459.png" width="400px" />

Teachable Machineは音声でもモデルを作れるので、気になる人はそちらも試してみてください。

PCやスマホもセンサーとして使うことが出来ますので、obnizで今回さわったセンサーに加えて

- カメラ（視覚）
- マイク（音）

もこのような形で使える手札になりました。

お疲れ様でした！

## 他の技術とTeachable Machineを組み合わせた例

プロトアウトスタジオの受講生の記事抜粋です。

- LINE Bot
  - [憧れのギニュー特戦隊の誰に似てるか判定するLINEbotを作ったから、ぜってぇ見てくれよなっ！ - Qiita](https://qiita.com/Teru_3/items/109517e6a6e3b761285d)
  - [現役、理学療法士が姿勢の画像を送るとその姿勢について教えてくれるLINE botを作った - Qiita](https://qiita.com/yusei2629/items/da07d877a98c94abb3c9)
- obniz
  - [画像から機械学習したモデルで、酔っ払っているかどうかを判断してアウトだったら警報色ライトをつけた - Qiita](https://qiita.com/Sugizo50073508/items/c34df866fb46276d6ade)

---

**[◀ 目次ページに戻る](../readme.md)**
