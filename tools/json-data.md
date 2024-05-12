# データの中から特定の数値のみ取り出して使う方法: JSONデータの扱いについて


センサーや、APIでデータを取得したとき、図のように複数のデータが入れ子になった構造の形式、「JSON形式」でデータが返ってくることがあります。

ここではJSONデータの取扱について説明します。

<a href="https://gyazo.com/19e6853559ea5c1354c612a188e7dc18"><img src="https://i.gyazo.com/19e6853559ea5c1354c612a188e7dc18.png" alt="Image from Gyazo" width="432"/></a>



何もせずにデータを使おうとすると......

<a href="https://gyazo.com/bc784ede411be0e701fd0fd9841b88a2"><img src="https://i.gyazo.com/bc784ede411be0e701fd0fd9841b88a2.png" alt="Image from Gyazo" width="408"/></a>

こうなってしまいます。



**数字だけを取り出すにはどうしたらいいでしょう？**


### ノードが渡すメッセージ「msg」って何？

Node-REDのノードは、左から右へメッセージ「msg」を渡します。

obniz repeatノードのmsgの中身をみてみましょう。

```json
{"payload":{"humidity":56.6,"temperature":26.78},"_msgid":"33d37c2cab810345"}

```

このような形式のデータをJSONといいます。


図にするとこんな構造になっています。
<a href="https://gyazo.com/4c7275a23caf7364cc657954c89eee47"><img src="https://i.gyazo.com/4c7275a23caf7364cc657954c89eee47.png" alt="Image from Gyazo" width="350"/></a>


今、msgの中のpayloadの中身が丸々テキストに表示されている状態です。
`{"humidity":56.6,"temperature":26.78}`


changeノードをつかって、数字のみの値を渡すようにしましょう！


 1. changeノードを配置する

<a href="https://gyazo.com/cb595807ffc979383f0229e15fb991ea"><img src="https://i.gyazo.com/cb595807ffc979383f0229e15fb991ea.png" alt="Image from Gyazo" width="500"/></a>

2. パスをコピーする

<a href="https://gyazo.com/2a4476e189515b7858f6c0bd14e56bbe"><img src="https://i.gyazo.com/2a4476e189515b7858f6c0bd14e56bbe.png" alt="Image from Gyazo" width="312"/></a>

3. changeノードの代入する値を設定する。

msgに変更し、先ほどコピーしたパスを貼り付ける。

<a href="https://gyazo.com/dae413fefd17d4b9911329a1b540db0e"><img src="https://i.gyazo.com/dae413fefd17d4b9911329a1b540db0e.png" alt="Image from Gyazo" width="519"/></a>




これで、JSON内に含まれる必要なデータを取り出すことができます。