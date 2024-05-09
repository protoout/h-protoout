# obnizをはじめよう


 - **インジケータ**(対象の状態を標示する装置)によって、情報を表示・通知する。: LED
  - **センサ**によって、光や温度といった環境情報を取得したり、変化を検知したりする。: 超音波距離センサ
  - **アクチュエータ**（動力源と機構部品を組み合わせて機械的な動作を行う装置）によって、実際のモノを動かす。: サーボモーター
 

obnizが提供するパーツライブラリを使って、簡単に動作を試すことができます。
ひとつひとつ試していきましょう！

## やってみよう

## 【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意
- **配線のときは必ず電源を抜くこと！**
- 配線は図をしっかり見て間違えがないか確認をしてから最後にUSBケーブルをさして電源を供給しましょう。
- 極性に注意
  - 扱うセンサーやアクチュエーターは極性があるかないか（プラスマイナスの電流の向き）を注意しましょう。極性を間違えて配線をするとデバイスが熱を持って高温になったり、壊れたりする場合があります。
- 怪我注意
  - 扱い方を間違える怪我や火傷をする場合があります。注意レベルを上げましょう。
- 破損注意
  - 扱い方を間違えるとデバイスを壊す場合があります。注意レベルを上げましょう。
- 壊してしまった場合
  - obniz本体やパーツが熱くなっている場合があります。取り外す場合は注意しましょう。
  - 壊しても落ち込まずに！
  - たいてい誰でも1回は壊します。
  - パーツ自体はそれほど値段もしないので、勉強代と思っていきましょう。
- プログラムを起動しっぱなしにしない
  - プログラムを起動したまま≒電気が通電しっぱなしの状態です。センサーなどがショートしてしまって破損や怪我に繋がる恐れがあります。
  - 別のセンサーやアクチュエーターを試す際は、 必ず「処理停止用フロー」をクリックしてから進めるようにしてください。
  - 新たなプログラムを起動する際は、毎回必ずobnizディスプレイにQRコードとobniz IDが表示されていることを確認してください。


## 1. 開発準備

**obniz IDを（手元に）メモしておきましょう！**

### 1-1 Node-REDにobnizノードをインストール
1. Node-REDを開いてください。

2. Node-REDの右上のメニュー（三本線）からパレットの管理を選びます。
   
   <a href="https://gyazo.com/87c62740eab97d764bacb3d3deb08c2d"><img src="https://i.gyazo.com/87c62740eab97d764bacb3d3deb08c2d.png" alt="Image from Gyazo" width="372"/></a>

3. 「ノードを追加」をクリックし「obniz」で検索してください。
   
   検索結果から`node-red-contrib-obniz`の「ノードを追加」を押してください。  
   （vnがついて**いない**方です！）
   
   <a href="https://gyazo.com/44977736c5df5749bfeb4102fc7e1d37"><img src="https://i.gyazo.com/44977736c5df5749bfeb4102fc7e1d37.png" alt="Image from Gyazo" width="500"/></a>

4. Node-REDの左側の「その他」の中に青いobnizノードが表示されていれば準備完了です。
   
   <a href="https://gyazo.com/1dc3e137af72509caed03e378f2861e3"><img src="https://i.gyazo.com/1dc3e137af72509caed03e378f2861e3.png" alt="Image from Gyazo" width="166"/></a>

obnizのノードはこんなときに使います。
- obniz repeat・・・常にデータを取り続けたいとき  
  例）温度センサー、距離センサー、照度センサーなどのセンサが検知したデータを一定間隔で取得し続ける、など。  

- obniz function・・・フロー上のきっかけでなにか動作させたいとき  
  例）LINE Botが受け取ったメッセージをきっかけに温度を取得する、など。

参考ページ：[Node-REDのobnizノードがバージョンアップした！](https://qiita.com/wicket/items/e150e78cd787da03493e)


### 1-2 「処理停止用フロー」を読み込む

Node-RED上で起動しているobnizのプログラムを止めるためのノードを準備します。
新しく別のフローを作るとき、かならず処理停止用フローを入れて、いつでもobnizを停止できる状態にしてください。
* 今は今ひとつピンとこないかもしれませんが...あとで「こういうことね」と、わかりますので今は手順に沿って進めましょう！


以下の手順で自身のNode-RED上に読み込みを行ってください。 


1. 下記のコードをすべてコピーしてください。

```json
[{"id":"cb1d6d3a.017e1","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":610,"y":140,"wires":[]},{"id":"11a346f0.5a4c19","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"msg.payload = \"close\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":440,"y":140,"wires":[["cb1d6d3a.017e1"]]},{"id":"76e43759.3dff68","type":"inject","z":"d9dba4a1.01f228","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":260,"y":140,"wires":[["11a346f0.5a4c19"]]}]
```

Node-REDの右上のメニュー（三本線）から読み込みを選びます。

<a href="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c"><img src="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c.png" alt="Image from Gyazo" width="372"/></a>

      

コピーしたコードを貼り付けます  
<a href="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a"><img src="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a.png" alt="Image from Gyazo" width="372"/></a>


■ 読み込み結果  
<a href="https://gyazo.com/ac38f368a5f4fefc730b30c4b6984944"><img src="https://i.gyazo.com/ac38f368a5f4fefc730b30c4b6984944.png" alt="Image from Gyazo" width="300"/></a>

1. `obniz function` ノードをダブルクリックで開き、プロパティの「新規に obniz を追加…」の右に表示されている「+」ボタンを押下してください。
   
<a href="https://gyazo.com/65b431b68f96a649539a319ce6e82143"><img src="https://i.gyazo.com/65b431b68f96a649539a319ce6e82143.png" alt="Image from Gyazo" width="657"/></a>


2. 表示されたプロパティ画面で、以下のとおり設定し「追加」を押下してください。  
   - obniz ID：自分のobniz ID  
   - device type：obnizBoard 1Y

   
   <a href="https://gyazo.com/c9e7dd06bccd6c2ab9ea6e0d1bd16f53"><img src="https://gyazo.com/c9e7dd06bccd6c2ab9ea6e0d1bd16f53.png" alt="Image from Gyazo" width="500"/></a>

3. obniz-functionノードを編集のプロパティ画面に戻ったら、「obniz」に前工程で設定したobniz IDが設定されていることを確認し、「完了」を押下してください。
   
   <a href="https://gyazo.com/593d9ee6524567b902dde5a842a46745"><img src="https://i.gyazo.com/593d9ee6524567b902dde5a842a46745.png" alt="Image from Gyazo" width="500"/></a>

【見てみよう】  
`obniz function`ノードをもう一度開き、中身を見てみましょう。  
コードの内容は以下のとおりとなっています。  
（実際のコードにはコメントはつけていません。）  

```javascript
msg.payload = "close"; //msg.payloadに"close"を格納→debugに"close"と表示されます
await obniz.wait(1000); //1000ミリ秒＝1秒obnizの処理を待機 
obniz.close(); //意図的にclose()関数を呼ぶことで通信を切断

return msg;
```

このように、Node-REDでobnizを使用する場合、ノードの中にコードを書く必要があります。  
これ以降に読み込むノードにも同じようにコードが設定されていますので、  
JSONコードを読み込んだ後にそれぞれのノードを開いてコードを確認してみてください。  





---

**[◀ 目次ページに戻る](../readme.md)**
