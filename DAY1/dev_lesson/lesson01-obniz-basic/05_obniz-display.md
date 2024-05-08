# obnizについているディスプレイを使ってみよう

LEDなど他のページですでに試していますが、

改めてobnizのディスプレイの使い方について触れていきます。


### **新しいことをはじめる前に※**  

[新しいことをはじめる前に](../before-start.md)この手順を行いましょう。


## 1.obnizのディスプレイの使い方

1. パレットから

- injectionノード
- obniz functionノード
- debugノード

<a href="https://gyazo.com/7fa3c7aa64ed04f781179a09fd38c255"><img src="https://i.gyazo.com/7fa3c7aa64ed04f781179a09fd38c255.png" alt="Image from Gyazo" width="464"/></a>

2. obniz functionノードのコードに以下を記載

```javascript

obniz.display.clear();//画面を消去
obniz.display.print(msg.payload);//表示したいテキスト

```

3. injectionノードを以下のように設定

「文字列」に設定し、
<img src="https://i.gyazo.com/55b213766fe04898d7926cc85d7738d3.png" width="500">

テキスト`Hello!`を入力してください。
<a href="https://gyazo.com/31c4c8e6af60165ba8017d2a9ade296b"><img src="https://i.gyazo.com/31c4c8e6af60165ba8017d2a9ade296b.png" alt="Image from Gyazo" width="500"/></a>

4. デプロイ後、injectionノードをクリックしてディスプレイにテキストが出ればOKです。
<a href="https://gyazo.com/03c351fabc467739a062d523f9a2622d"><img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" alt="Image from Gyazo" width="500"/></a>


[ディスプレイについて公式ドキュメント](https://docs.obniz.com/ja/reference/common/display#%E6%8F%8F%E7%94%BB%E9%96%A2%E6%95%B0)


## 2.演習

### 2-1. injectionノードを複数つなげてディスプレイの文字を切り替えよう
- Hello!
- Good Morning

### 2-2. 【応用】スピーカーやLEDとディスプレイを一緒に使って、楽しいものを作ってみよう！

[参考記事: Node-RED から obniz ノードをつかってクリスマスソング＆キラキラ＆顔文字ダンスさせる！](https://qiita.com/tseigo/items/56c78be82b6276825ca6)


---

**[◀ 目次ページに戻る](../readme.md)**