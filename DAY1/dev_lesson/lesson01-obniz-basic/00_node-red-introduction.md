# Node-RED: 基本的な操作とフローのつくりかたを学ぼう

## 1.Node-REDの全体像

Node-REDは基本的に **「左から右に」** がキーワードです！

まずは、画面の見方と、Node-REDで重要な概念について説明をします。

### 1-1. ノードとフロー

Node-REDは左から右にノード（機能をもったパーツのようなもの）を繋ぐことでプログラムを作ります。
ノードをつないだものを、フローと呼びます。

各ノードは、次のノードに、メッセージ（msg）を渡します。


この様なイメージです。

<a href="https://gyazo.com/0375f43aa246a15c6326c709b351e057"><img src="https://i.gyazo.com/0375f43aa246a15c6326c709b351e057.png" alt="Image from Gyazo" width="406"/></a>

左から2番目のノードが、3番目のノードに「5」を渡したとします。

3番目のノードは、数字の後ろに「月」を追加する役割を持っています。

↓
↓

3番目のノードは、2番目のノードからもらった「5」に「月」を追加した「5月」というmsgを4番目のノードに渡します。


このような感じで、各ノードはmsgを受け取り、自分の役割に応じてmsgを変更/削除/作成して、次のノードに渡します。



### 1-2. 画面の見方

<img src="https://i.gyazo.com/04dcf5b6013c869a558078e4e4b4772d.png" width="500">

左から、パレット・ワークスペース・サイドバーという名前がついています。それぞれの役割は...


1. パレット：利用できるノードの一覧が表示されています。

2. ワークスペース: 方眼ノートのようなマス目がついているエリア。ノード同士をワイヤーで繋ぐことによってフローを開発する場所。

3. サイドバー: ノードについての情報や、debugノード（後ほど詳細を説明します）で受け取ったデータの表示など、色々な詳細情報を見るためのエリアです。




## 2. 操作の練習をしよう: ノードを置いて、つないで、削除する

### 2-1. やってみよう
injectノードをとdebugノードをつなぎ、ボタンを押したら「こんにちは」と出るフローを作ってみましょう。

1. 左のパレットからinjectノードをとdebugノードをドラッグ＆ドロップし、ワークスペースに置く。その後injectノードの右側の点から、debugノード左側の点に線を引っ張る。
<a href="https://gyazo.com/c67a3af6f4f2c0427547f88747f7c6fc"><img src="https://i.gyazo.com/c67a3af6f4f2c0427547f88747f7c6fc.gif" alt="Image from Gyazo" width="500"/></a>

**ノードを探すときは、パレット上部の検索窓を使うと便利🔎**
<a href="https://gyazo.com/10c998efdb3275dcab85851d343322bf"><img src="https://i.gyazo.com/10c998efdb3275dcab85851d343322bf.png" alt="Image from Gyazo" width="249"/></a>

<img src="https://i.gyazo.com/39eddfeebf8cb98516014a8c9a6527bb.png" width="500">

2. injectノードを図のように「文字列」に設定
<img src="https://i.gyazo.com/55b213766fe04898d7926cc85d7738d3.png" width="500">

3. 「こんにちは」と記入。
<img src="https://i.gyazo.com/7c2cf66b5e9e404eefaf0bd0cd13b525.png" width="500">

4. ノードの名前をわかりやすく変更する。「あいさつ」とします。
<a href="https://gyazo.com/56cc0f9e58c6810ee7014d890150596f"><img src="https://i.gyazo.com/56cc0f9e58c6810ee7014d890150596f.png" alt="Image from Gyazo" width="500"/></a>

5. 右上デプロイをクリック
<a href="https://gyazo.com/be94e8717dab3e6af8247a9fa5a49214"><img src="https://i.gyazo.com/be94e8717dab3e6af8247a9fa5a49214.png" alt="Image from Gyazo" width="500"/></a>

6. サイドバーの虫マークをクリックし、コンソールを表示。
<a href="https://gyazo.com/98b101ebb9c768f020e2641caef22f46"><img src="https://i.gyazo.com/98b101ebb9c768f020e2641caef22f46.png" alt="Image from Gyazo" width="500"/></a>

7. injectノードの左側にあるボタンをクリックし、コンソールに「こんにちは」と出ていればOK
<a href="https://gyazo.com/1b58ac73c3c40b215516387ec036c860"><img src="https://i.gyazo.com/1b58ac73c3c40b215516387ec036c860.gif" alt="Image from Gyazo" width="1000"/></a>


Node-REDの操作は基本的に以下の繰り返しとなります。

1. 左のパレットから、右隣のワークスペースにノードを配置 
2. ノード同士を左から右へつなぐ
3. 各ノードの設定を行う
4. デプロイする
5. 正しい動作をしているか確認する


### 2-2. ノードや、接続の削除

1. 不要なノードを削除する: ノードを選択し、deleteキーを押す

2. 間違った接続をしたとき: 削除したい線を選択し、オレンジに変わったらdeleteキーを押す




---

**[◀ 目次ページに戻る](../readme.md)**