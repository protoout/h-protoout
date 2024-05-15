
# マニュアル: obnizのディスプレイ


1. ノードを配置し以下のように接続

- injectノード
- changeノード
- obniz functionノード
- debugノード

<a href="https://gyazo.com/f9aa30868da8d731b2392df69b65849a"><img src="https://i.gyazo.com/f9aa30868da8d731b2392df69b65849a.gif" alt="Image from Gyazo" width="600"/></a>


2. obniz functionノードのコードに以下を記載

```javascript

obniz.display.clear();//画面を消去
obniz.display.print(msg.payload);//msg.payloadの内容をディスプレイに表示

```

3. changeノードを以下のように設定

「文字列」に設定し、テキスト`Hello!`を入力してください。

<a href="https://gyazo.com/f23286bfca01518a135be99eb623abfe"><img src="https://i.gyazo.com/f23286bfca01518a135be99eb623abfe.gif" alt="Image from Gyazo" width="600"/></a>



5. 結果

injectノードをクリックしてディスプレイにテキストが出ればOKです。

<a href="https://gyazo.com/03c351fabc467739a062d523f9a2622d"><img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" alt="Image from Gyazo" width="500"/></a>

■ 参考資料
[obnizの公式ドキュメント: ディスプレイ](https://docs.obniz.com/ja/reference/common/display#%E6%8F%8F%E7%94%BB%E9%96%A2%E6%95%B0)


