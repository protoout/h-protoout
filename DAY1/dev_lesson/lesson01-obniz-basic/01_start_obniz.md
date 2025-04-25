> [!WARNING]
> **使う場所に注意！**  
> obniz Boardはノートパソコンの上に置かず、机の上など電気を通さない場所に置きましょう。
  
## obnizとは?

obnizは、手軽にIoTサービスを構築するための仕組みです。  
IoTに必要なデバイス上のファームウェア、クラウドとの通信と暗号化、クラウド上でのデバイス認証と管理機能は全て、obnizより提供されます。

> [!NOTE]
> 会社の名前でもあり、システムの名前でもあります

  
### 私たちが使うobniz Board 1Y
  
obniz Board 1Y は obniz の公式デバイスです。いわゆる**マイコンボード**です。小型のコンピューターにハードウェアをつくるのに必要なパーツがちょこちょこ付いたものです。

***以降 obniz Board のことを長いので 「**obniz**」 と呼びます***  

obniz は専用のクラウドを使ってインターネット経由で簡単に電子部品を操作することができます。
具体的には Node-RED に書いたプログラムを使って obniz を制御します。

<img src="https://github.com/user-attachments/assets/80eb5ff1-ca20-4f2b-ae99-e60f9396aca0 " width="70%" />

> [!TIP]
> 実はこのインターネットにつなぐのは結構めんどくさい...！obniz は他のマイコンボードに比べクラウド連携が非常に簡単です。  
  
ちなみに他の有名なマイコンボードは次の通りです。聞いたことあるものはありますか？  
- Arduino（アルドゥイーノ）
- Raspberry Pi（ラズベリーパイ）
- M5Stack
- microbit
- ESP32 / ESP8266
  
----  
  
## Node-RED で obniz を動かしてみる


では早速 obniz を動かしてみましょう。まだセンサーは使いません！  
電源をつなぎ QR コードとID(XXXX-XXXXの数字)が表示されている状態からスタートします  
  
> [!WARNING]
> **obniz ID はSNSなどには公開しないようにしましょう！**  
  

### 1. Node-RED に obniz 用のノードを追加する  
  
メニューバーから「パレットの管理」を選択  
  
<img width="500" alt="image" src="https://github.com/user-attachments/assets/451ada84-541f-4b37-8bed-4422639099c5" />
  
「ノードを追加」タブを選び「obniz」と検索すると、 `node-red-contrib-obniz` が出てくるので、「ノードを追加」を選択  
  
<img width="500" alt="image" src="https://github.com/user-attachments/assets/6f2faea1-13e9-466c-8cce-1c1d339e1803" />
  
「閉じる」からフロー設計の画面に戻ります。

### 2. 使うノードとつなぎ方

ノードの繋ぎ方

- `injectノード`
- `changeノード`
- `obniz-functionノード`
- `debugノード`  
  
obniz-functionノードはノードの一覧の下の方の「その他」に入っています。  
  
<img width="300" alt="image" src="https://github.com/user-attachments/assets/fc966a02-1f8f-47ee-a3de-9817f1967c11" />  
  
<img src="https://i.gyazo.com/f9aa30868da8d731b2392df69b65849a.gif " width="90%" />  


## 3. 各ノードの設定方法

### 3-1. `obniz-functionノード`

ノードをダブルクリックして「＋」ボタンから新規に obniz 設定ノードを追加します  

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/db06cb0d-1813-4417-831b-46e504383547" />

`obniz ID` に obniz に表示されている番号を入れます(ハイフンは有/無どちらでも大丈夫)  
`device type` を obniz 1Y にします  
  
<img width="50%" alt="image" src="https://github.com/user-attachments/assets/f89dd30f-53df-407c-9224-a01015660c45" />  
  

コードに以下を記述  

```js
obniz.display.clear();//画面を消去
obniz.display.print(msg.payload);//msg.payloadの内容をディスプレイに表示
```

### 3-2. `changeノード`

「文字列」に設定し、テキスト`Hello!`を入力してください。

<img src="https://i.gyazo.com/f23286bfca01518a135be99eb623abfe.gif" width="90%" />  

## 4. 結果

`injectノード`をクリック(左の四角いアイコン)してディスプレイにテキストが出れば OK です！
  
<img src="https://i.gyazo.com/03c351fabc467739a062d523f9a2622d.jpg" width="90%" />

インターネット経由で obniz を操作しました！！

## 5. ちょっと待った！接続を切りましょう✂

Node-RED の場合、Node.js のプロセスは起動し続ける仕様なため、プログラムの起動ではなく接続の解除を行って停止を行います。  
要するに、**実はまだ接続は残っているのでノードを使ってちゃんと切りましょう**、ということです！  
  
`obniz-closeノード`を使います。`injectノード`と繋いで実行します。  
  
<img src="https://github.com/user-attachments/assets/2bf4e492-0b16-4f9e-bb93-69c5b2995ec0" width="90%" />   
  
上手くいくと、obnizのディスプレイが元の QR コードと ID の画面に戻ります
> [!CAUTION]
> **以降も新しいノードを実行する場合は、毎回必ずこのプロセスを実行しましょう！**  
> 
---- 
[戻る](../)
