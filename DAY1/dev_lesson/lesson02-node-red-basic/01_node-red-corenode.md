# Node-REDでよくつかわれる「コアノード」を学ぼう

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

- changeノード: 
- switchノード: 

### やってみよう
図のようにノードをつなぎ、

<img src="https://i.gyazo.com/899837fd64bfcfb1b23cd574edbf4775.png" width="500px" alt="Image 3">

1. 3つのinjectノードを配置。それぞれのノードは、payloadにりんご・みかん・バナナと入力。


2. 3つのinjectノードからswitchノードにつなぐ。

    - りんごの場合: 赤を出力
    - みかんの場合: オレンジを出力
    - バナナの場合: 黄色を出力


3. debugノードにレスポンスを表示する


## 3. templateノード

