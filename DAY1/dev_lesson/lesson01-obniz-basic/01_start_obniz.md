> [!WARNING]
> **使う場所に注意！**  
> obniz Board はノートパソコンの上に置かず、机の上など電気を通さない場所に置きましょう。

# 私たちが使う obniz Board / obniz Board 1Y
  
obniz Board は obniz の公式デバイスで、いわゆる**マイコンボード**です。小型のコンピューターにハードウェアをつくるのに必要なパーツがちょこちょこ付いたものです。


obniz Board は専用のクラウドを使ってインターネット経由で簡単に電子部品を操作することができます。
この授業では Node-RED に書いたプログラムを使って obniz Board を制御します。

<a href="https://gyazo.com/930f11fc4840fb168338e370d0df6e37"><img src="https://i.gyazo.com/930f11fc4840fb168338e370d0df6e37.png" alt="Image from Gyazo" width="450"/></a>


> [!TIP]
> 実はこの「インターネットにつなぐ」というのは結構めんどくさい...！obniz Board は他のマイコンボードに比べクラウド連携が非常に簡単とされています。  
  
ちなみに他の有名なマイコンボードは次の通りです。聞いたことあるものはありますか？  
- Arduino（アルドゥイーノ）
- Raspberry Pi（ラズベリーパイ）
- M5Stack
- microbit
- ESP32 / ESP8266
  
----  
  
# Node-RED で obniz Board を動かしてみる


では早速 obniz Board を動かしてみましょう。まだセンサーは使いません！  
電源をつなぎ QR コードとID(XXXX-XXXXの数字)が表示されている状態からスタートします  
  
> [!WARNING]
> **obniz ID はSNSなどには公開しないようにしましょう！**
 
## 1. Node-RED に obniz Board 用のノードを追加する  
  
メニューバーから「パレットの管理」を選択  
>   
> <a href="https://gyazo.com/d58d86af3b089eda430275e592749e0e"><img src="https://i.gyazo.com/d58d86af3b089eda430275e592749e0e.png" alt="Image from Gyazo" width="450"/></a>

  
「ノードを追加」タブを選び「obniz」と検索すると、 `node-red-contrib-obniz` が出てくるので、このノードで「ノードを追加」を選択  
>    
> <a href="https://gyazo.com/cdf591f25db082a498dd96ee76bc25e6"><img src="https://i.gyazo.com/cdf591f25db082a498dd96ee76bc25e6.png" alt="Image from Gyazo" width="450"/></a>

  
「閉じる」からフロー設計の画面に戻ります。

## 2. 使うノードとつなぎ方

ノードの繋ぎ方

- `injectノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`  

これらのノードを配置していきます。

> <img src="https://i.gyazo.com/f9aa30868da8d731b2392df69b65849a.gif " width="90%" />
>   
> `injectノード`や`changeノード`は配置すると`タイムスタンプ`や`set msg.payload`など名前が変わります。
  
> <a href="https://gyazo.com/4e7fdc790c8088c3bc0d0d2f0233a4bc"><img src="https://i.gyazo.com/4e7fdc790c8088c3bc0d0d2f0233a4bc.png" alt="Image from Gyazo" width="450"/></a>
>   
> なお、`obniz-functionノード`はノードの一覧の下の方の「その他」に入っています。    


## 3. 各ノードの設定方法

### 3-1. `obniz-functionノード`

ノードをダブルクリックして「＋」ボタンから新規に obniz 設定ノードを追加します  
>  
> <a href="https://gyazo.com/9132a1b70275ea6951c1461f3f283af2"><img src="https://i.gyazo.com/9132a1b70275ea6951c1461f3f283af2.png" alt="Image from Gyazo" width="450"/></a>

`obniz ID` に obniz Board に表示されている番号を入れます(ハイフンの有無はどちらでも大丈夫)  
  
`device type` を obniz または obniz 1Y にします。  
>   
> <a href="https://gyazo.com/a5eeacd7e0f24eb40b6f79e826951f61"><img src="https://i.gyazo.com/a5eeacd7e0f24eb40b6f79e826951f61.png" alt="Image from Gyazo" width="450"/></a> 
  
追加（または更新）を押すと再び同じ画面に戻ってきます。今度は `obniz` のところはご自身で設定した内容が反映されています。  
<a href="https://gyazo.com/29d2c198b52828d12502f88d709ce103"><img src="https://i.gyazo.com/29d2c198b52828d12502f88d709ce103.png" alt="Image from Gyazo" width="450"/></a>
  
  
この画面の「コード」の部分に以下を記述  

```js
obniz.display.clear();//画面を消去
obniz.display.print(msg.payload);//msg.payloadの内容をディスプレイに表示
```

### 3-2. `changeノード`

「文字列」に設定し、テキスト`Hello!`を入力してください。
> 
> <img src="https://i.gyazo.com/f23286bfca01518a135be99eb623abfe.gif" width="90%" />  


## 4. 結果
右上の`デプロイ`を押したらください準備完了です。

> `injectノード`をクリック(左の四角いアイコン)してディスプレイにテキストが出れば OK です！
>   
> <a href="https://gyazo.com/71aca56a3b8033307dfbffdcd31cabb7"><img src="https://i.gyazo.com/71aca56a3b8033307dfbffdcd31cabb7.gif" alt="Image from Gyazo" width="450"/></a>
  
> <img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" width="450" />

インターネット経由で obniz Board を操作しました！！

## 5. ちょっと待った！接続を切りましょう  

このままでは Node-RED でつくったプログラムが実行されたままです。Node-RED から obniz Board との接続を切るための指示を出しましょう。

  
`obniz-closeノード`を使います。新たに`injectノード`も用意し繋ぎます。  
  

<a href="https://gyazo.com/2c04e76a6bae0fb96cdd0dca7bf5d49b"><img src="https://i.gyazo.com/2c04e76a6bae0fb96cdd0dca7bf5d49b.png" alt="Image from Gyazo" width="450"/></a>
  
`obniz-closeノード`も obniz ID を指定する必要がありますが既に先ほど`obniz-functionノード`で登録したものがあるはずです。  
  
> [!IMPORTANT]
> **重要です！obniz ID は一度設定すれば以降は新規でつくる必要はありません！**  
> 他の obniz 関連のノード(`obniz functionノード`や後で出てくる `obniz repeatノード`など)を用意したときには、既に作成した obniz ID を選びましょう。  
   
<a href="https://gyazo.com/b1b26fa6151ec679905a7fca9a0096d0"><img src="https://i.gyazo.com/b1b26fa6151ec679905a7fca9a0096d0.png" alt="Image from Gyazo" width="450"/></a>


再度デプロイして`injectノード`をクリックすると`obniz-functionノード`と`obniz-closeノード`に赤い四角いアイコンが表示されます。  
  
> <a href="https://gyazo.com/641b56ba2d2cdbeab7a4109cd4f55419"><img src="https://i.gyazo.com/641b56ba2d2cdbeab7a4109cd4f55419.png" alt="Image from Gyazo" width="450"/></a>
> これが obniz Board と接続を切った状態です。

  
上手くいくと、obniz Board　のディスプレイも元の QR コードと ID の画面に戻ります  
  
<a href="https://gyazo.com/ae81bec5f4c3e1ffda2b33be422469de"><img src="https://i.gyazo.com/ae81bec5f4c3e1ffda2b33be422469de.jpg" alt="Image from Gyazo" width="450"/></a>

> [!CAUTION]
> **以降も新しいノードを実行する場合は、毎回必ずこの「接続を切る」プロセスを実行しましょう！**  
> 
---- 
[◀ Lesson1に戻る](../)
