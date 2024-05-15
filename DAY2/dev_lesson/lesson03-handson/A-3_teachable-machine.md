# A-3. ハンズオン: Teachable Machineで独自モデルの作成と画像判定

Teachable MachineはGoogleが公開している機械学習を楽しく使えるノーコードツールです。



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

## 1. Teachable Machineでモデル作成

指示に沿って進んでみましょう。

- 「Get Started（使ってみる）」をクリック

> <img src="https://i.gyazo.com/4aa6aa6236a2b6af6595f143cdf5fe68.png" width="400px" />

- 画像プロジェクトを選択します。

> <img src="https://i.gyazo.com/3102e9b541cad46c885439ddee701963.jpg" width="400px" />

- 標準の画像モデルを選択します。

> <img src="https://i.gyazo.com/4fdfb10b7ad728fea7a7d6a9b4a31db7.png" width="400px" />


## 利用するノードのインストール

- `node-red-contrib-teachable-machine`
    - teachable-machineで作成したモデルを使用するためのノード このノードは「image Project」のみに対応しているようです。

- `node-red-contrib-browser-utils`
    - 自分のPCのカメラの写真データを読み込んでくれるノード

- `node-red-contrib-image-output`
    - 読み込んだ画像をNode-RED上に表示してくれるノード

> <img src="https://i.gyazo.com/f3d3f76405b85e266165ae625f4a99a4.gif" width="400px" />

> <img src="https://i.gyazo.com/04000b3380bb4ee0ac59e58d3ae6a827.png" width="400px" />

## Teachable Machine