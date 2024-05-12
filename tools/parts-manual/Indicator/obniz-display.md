
# マニュアル: obnizのディスプレイ

<details><summary>使い方をクリックで開く</summary>

1. ノードを配置し以下のように接続

- injectionノード
- obniz functionノード
- debugノード

<a href="https://gyazo.com/7fa3c7aa64ed04f781179a09fd38c255"><img src="https://i.gyazo.com/7fa3c7aa64ed04f781179a09fd38c255.png" alt="Image from Gyazo" width="464"/></a>

2. obniz functionノードのコードに以下を記載

```javascript

obniz.display.clear();//画面を消去
obniz.display.print(msg.payload);//msg.payloadの内容をディスプレイに表示

```

3. injectノードを以下のように設定

「文字列」に設定し、

<img src="https://i.gyazo.com/55b213766fe04898d7926cc85d7738d3.png" width="500">

テキスト`Hello!`を入力してください。

<a href="https://gyazo.com/31c4c8e6af60165ba8017d2a9ade296b"><img src="https://i.gyazo.com/31c4c8e6af60165ba8017d2a9ade296b.png" alt="Image from Gyazo" width="500"/></a>


5. 結果

injectionノードをクリックしてディスプレイにテキストが出ればOKです。

<a href="https://gyazo.com/03c351fabc467739a062d523f9a2622d"><img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" alt="Image from Gyazo" width="500"/></a>

■ 参考資料
[obnizの公式ドキュメント: ディスプレイ](https://docs.obniz.com/ja/reference/common/display#%E6%8F%8F%E7%94%BB%E9%96%A2%E6%95%B0)

</details>
