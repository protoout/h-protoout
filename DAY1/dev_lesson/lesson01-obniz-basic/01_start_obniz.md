> [!WARNING]
> **使う場所に注意！**  
> obniz Board はノートパソコンの上に置かず、机の上など電気を通さない場所に置きましょう。

# 私たちが使う obniz Board / obniz Board 1Y
  
obniz Board は obniz の公式デバイスで、いわゆる**マイコンボード**です。小型のコンピューターにハードウェアをつくるのに必要なパーツがちょこちょこ付いたものです。


obniz Board は専用のクラウドを使ってインターネット経由で簡単に電子部品を操作することができます。
この授業では Node-RED に書いたプログラムを使って obniz Board を制御します。

<img src="https://github.com/user-attachments/assets/80eb5ff1-ca20-4f2b-ae99-e60f9396aca0 " width="50%" />

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
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/451ada84-541f-4b37-8bed-4422639099c5" />

  
「ノードを追加」タブを選び「obniz」と検索すると、 `node-red-contrib-obniz` が出てくるので、このノードで「ノードを追加」を選択  
>    
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/6f2faea1-13e9-466c-8cce-1c1d339e1803" />
  
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
  
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/fc966a02-1f8f-47ee-a3de-9817f1967c11" />
>   
> なお、`obniz-functionノード`はノードの一覧の下の方の「その他」に入っています。    


## 3. 各ノードの設定方法

### 3-1. `obniz-functionノード`

ノードをダブルクリックして「＋」ボタンから新規に obniz 設定ノードを追加します  
>  
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/db06cb0d-1813-4417-831b-46e504383547" />

`obniz ID` に obniz Board に表示されている番号を入れます(ハイフンの有無はどちらでも大丈夫)  
  
`device type` を obniz または obniz 1Y にします。  
>   
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/f89dd30f-53df-407c-9224-a01015660c45" />  
  
更新を押すと再び同じ画面に戻ってきます。今度は `obniz` のところはご自身で設定した内容が反映されています。  
<img width="450" alt="image" src="https://github.com/user-attachments/assets/8143ee58-62bd-46bd-943b-60d8d57545ae" />
  
  
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
> <img src="https://github.com/user-attachments/assets/b735f182-7a9a-4663-977b-1a7534b852c2 " width="90%" />
  
> <img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" width="450" />

インターネット経由で obniz Board を操作しました！！

## 5. ちょっと待った！接続を切りましょう  

このままでは Node-RED でつくったプログラムが実行されたままです。Node-RED から obniz Board との接続を切るための指示を出しましょう。

  
`obniz-closeノード`を使います。新たに`injectノード`も用意し繋ぎます。  
  
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/571671eb-291d-4df3-b79c-85e7498bf6c9" />  
  
`obniz-closeノード`も obniz ID を指定する必要がありますが既に先ほど`obniz-functionノード`で登録したものがあるはずです。  
  
> [!IMPORTANT]
> **重要です！obniz ID は一度設定すれば以降は新規でつくる必要はありません！**  
> 他の obniz 関連のノード(`obniz functionノード`や後で出てくる `obniz repeatノード`など)を用意したときには、既に作成した obniz ID を選びましょう。  
   
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/45f4648c-8b6d-4891-a32f-2a8935e9c398" />

再度デプロイして`injectノード`をクリックすると`obniz-functionノード`と`obniz-closeノード`に赤い四角いアイコンが表示されます。  
  
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/3b303c67-aff7-4124-bdbb-8d9292bc1317" />
> これが obniz Board と接続を切った状態です。

  
上手くいくと、obniz Board　のディスプレイも元の QR コードと ID の画面に戻ります  
  
> <img width="450" alt="image" src="https://github.com/user-attachments/assets/eb49d4ee-5c8d-4b73-bb0e-39b870429bcc" />

> [!CAUTION]
> **以降も新しいノードを実行する場合は、毎回必ずこの「接続を切る」プロセスを実行しましょう！**  
> 
---- 
[◀ Lesson1に戻る](../)
