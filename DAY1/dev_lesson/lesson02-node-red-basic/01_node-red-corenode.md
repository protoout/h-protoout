# Node-REDでよくつかわれる「コアノード」を学ぼう

ここまで、よくわからないながらも資料に沿ってNode-REDの操作をしてきたと思います。


そろそろ、Node-REDの操作方法をきちんと学んで、

自分の思う通りに動かしたい！という気持ちが湧き出ているのではないでしょうか？



このパートでは、基本操作とよく使うノードの使い方や

GUI（視覚的なインターフェース）でデータを表示する方法を学びます。



Nore-REDでフローを組み立てるときによくつかう、コアノードを紹介します。


これらのコアノードは、Node-RED環境を作ったときデフォルトでインストールされています。

[公式リファレンス](https://nodered.jp/docs/user-guide/nodes)


## 1. injectノードとdebugノード: injectにはじまりdebugに終わる！？最頻出ノード

- injectノード: 左にある四角いボタンをクリックすると、設定した文字列や数字などのデータを出力するノード。
- debugノード: 前のノードから渡されたPayloadの値をコンソールに表示するノード。

### やってみよう
injectノードをとdebugノードをつなぎ、ボタンを押したら「こんにちは」と出るフローを作ってみましょう。

1. 図のようにinjectノードをとdebugノードを配置してつなぐ
<img src="https://i.gyazo.com/39eddfeebf8cb98516014a8c9a6527bb.png" width="500">

2. injectノードを図のように「文字列」に設定
<img src="https://i.gyazo.com/55b213766fe04898d7926cc85d7738d3.png" width="500">

3. 「こんにちは」と記入。
<img src="https://i.gyazo.com/7c2cf66b5e9e404eefaf0bd0cd13b525.png" width="500">

デプロイして挙動を確かめましょう！コンソール


## 2. changeノードとswitchノード: 

- changeノード: 左から来たmsgの中身を書き換えて右に渡すノード
- switchノード: 左から来たmsgの内容によって分岐させるノード

### やってみよう

1. 図のようにノードをつなぐ。

左から、
- 3つのinjectノード
- 1つのswitchノード
- 3つのchangeノード
- 1つのdebugノード
<img src="https://i.gyazo.com/899837fd64bfcfb1b23cd574edbf4775.png" width="500px" alt="Image 3">

2. 3つのinjectノードそれぞれ、payloadにりんご・みかん・バナナと入力。

<img src="https://i.gyazo.com/f09d0a4497cd1b51b19258e6920ffe87.png" width="500px" alt="Node-RED flow example">


3. switchノードを以下のように設定

<img src="https://i.gyazo.com/a29ba2158516ca45bad7012ac8da348e.png" width="500px" alt="Node-RED flow example">


4. 3つのchangeノードをそれぞれ以下のように設定
    - りんごの場合: 赤を出力
    - みかんの場合: オレンジを出力
    - バナナの場合: 黄色を出力

<img src="https://i.gyazo.com/faca776c0dd32f154c65c00b808ac22b.png" width="500px" alt="Node-RED flow example">

3. debugノードにレスポンスを表示する


## 3. templateノード

- templateノード: 左から来たmsgの中身を、任意のテンプレートにはめ込んで右に渡すノード

1. injectノード、templateノード、debugノードの順で配置し図のようにつなぐ
<img src="https://i.gyazo.com/0d12c5b28edac540a414072b315de952.png" alt="Image Description" width="500"/>


2. injectノードを下記のように設定
<img src="https://i.gyazo.com/d7da0207e61c3a718b3a4931b4867548.png" width="500">

3. templateノードの「テンプレート」に下記をコピペ
<img src="https://i.gyazo.com/cce969789dc087fda8d9ac8f41f46893.png" width="500" alt="Image 3">

テンプレートに記入する内容

```mustache

こんにちは！現在は{{payload}}です。Node-REDは楽しいですね！

```

4. デプロイし、injectノードのボタンをクリックして下記のように出てくれば成功です！
<img src="https://i.gyazo.com/a5b4701bb175bc2829453ccbb800f1cb.png
" alt="Image Description" width="500"/>


## 4. functionノード
JavaScriptをかくことができるノードです。既存のノードでできないときにこのノードを使います。

ビジュアルプログラミングツールは操作が簡単ですが、多くのそういったツールは簡単に扱える一方でできることが限られ、ある程度複雑なことをやろうとすると、「ツールの制約でできない」ということがしばしば起こります。


しかし、Node-REDはビジュアルプログラミングをベースとしながらもコードを記述できる自由度があり、既存のノードでは実現できない複雑な処理や特定の要件に対応することが可能です。

Node-REDはシンプルなタスクから複雑なプロジェクトまで幅広いニーズに対応できるプログラミングツールとなっています。



---

**[◀ 目次ページに戻る](../readme.md)**