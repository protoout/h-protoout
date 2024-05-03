# 1. サーボモーター

<a href="https://gyazo.com/d0c9462e27bc17845f5a14bb81080897"><img src="https://i.gyazo.com/d0c9462e27bc17845f5a14bb81080897.jpg" alt="Image from Gyazo" width="700"/></a>

<a href="https://gyazo.com/6e51a64cd7b7ddbf16a7937a8561ee3a"><img src="https://i.gyazo.com/6e51a64cd7b7ddbf16a7937a8561ee3a.jpg" alt="Image from Gyazo" width="700"/></a>

小規模なIoTでもっともよく使われる「アクチュエーター」の1つです。  
通常のモーターは電流を流すと回転し続けますが、サーボモーターは特殊な電流を流すことで「軸の位相を任意の角度に変化」させることができます。

設定可能な最大角度・回転トルク（強さ）・設定角度の細かさなどは、サーボモーターの性能によって大きく変わってきます。  
今回扱うのはホビー用途でもっとも汎用的なモデルです。

### 1-1. obnizとの接続

[![Image from Gyazo](https://i.gyazo.com/9e761676b8bffafd044339fdc26199dc.jpg)](https://gyazo.com/9e761676b8bffafd044339fdc26199dc)

以下をまず準備してください。

- サーボモーター
- ジャンパワイヤ白1本
- ジャンパワイヤ赤1本
- ジャンパワイヤ青1本
- ブレッドボード

[![Image from Gyazo](https://i.gyazo.com/7569445e6968343962bec179da49a56c.jpg)](https://gyazo.com/7569445e6968343962bec179da49a56c)

最初はサーボモーターとジャンパワイヤを接続：

- サーボモーター茶 - ジャンパワイヤ白
- サーボモーター橙 - ジャンパワイヤ赤
- サーボモーター黄 - ジャンパワイヤ青

[![Image from Gyazo](https://i.gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461.png)](https://gyazo.com/fe68ac7ea4bd5bd203b84ffd06ec8461)

[![Image from Gyazo](https://i.gyazo.com/78e42de894f9c2714afc006e27a0f521.png)](https://gyazo.com/78e42de894f9c2714afc006e27a0f521)

次にジャンパワイヤとobnizを接続：

- ジャンパワイヤ赤 - プラス
- ジャンパワイヤ白 - マイナス
- ジャンパワイヤ青 - obniz 2

このように接続できましたか？

最後に、回転してるかわかりやすいようにサーボにプラスチックパーツをつけましょう。（このパーツのことを**サーボホーン**といいます）  
好きな形状のもので構いません。

<a href="https://gyazo.com/c6cce3627ad4d4e6687e740d2fe2c27b"><img src="https://i.gyazo.com/c6cce3627ad4d4e6687e740d2fe2c27b.jpg" alt="Image from Gyazo" width="700"/></a>

### 1-2. ドキュメントページから実行

[![Image from Gyazo](https://i.gyazo.com/55e78fe8109fb6fc1aac86d150ed8a8e.gif)](https://gyazo.com/55e78fe8109fb6fc1aac86d150ed8a8e)

[部品を使う：サーボモーターを回す - obniz Docs](https://obniz.com/ja/doc/guides/obniz-starter-guide/parts-library/servo-motor)

上記にアクセスし、スクロールして一番下にあるサンプルでobniz IDを入力し、`実行`ボタンをクリックしてポップアップを開き、スライダーを動かすことでサーボモーターが連動して動くことを確認してください。

<details>
<summary>(補足)obniz Boardで過電流警告が出た場合の対策</summary>

[![Image from Gyazo](https://i.gyazo.com/87b44ab127c5f03b63ccce1b9eab71b1.png)](https://gyazo.com/87b44ab127c5f03b63ccce1b9eab71b1)

> **heavy output. output voltage is too low when driving high** が連続して発生することがあります。  
> 単純にこのスクリプトを再起動するか、ブレッドボードを経由して配線を行うかすると改善する場合があります。  
> ジャンパワイヤの抵抗値による過電流か、サーボモーターの個体差（相性）で発生する、ということが多いようです。

どうしても上記が発生してしまう場合は、

- ジャンパワイヤ（何色でもよい）2本
- ブレッドボード

を用意し、以下のように「もともと接続されていた赤いジャンパワイヤ」をobnizから取り外し、2本のジャンパワイヤを使ってブレッドボード上を経由させてobnizの1番ピンに接続してみてください。

[![Image from Gyazo](https://i.gyazo.com/1da8306c935fd4183c9d331a6cad8d0f.png)](https://gyazo.com/1da8306c935fd4183c9d331a6cad8d0f)

</details>

<details>
<summary>(補足)ハンチングについて</summary>

サーボモーターにはその構造上「ハンチング」という現象が起こります。  
これは特定の位置で停止した場合に、細かい振動を起こして完全には停止しない現象です。とくに0度や180度といった端点で発生することが多いため、以下のNode.jsでスクリプトを書くときなどは注意してください。  
（上記ドキュメントページのスライダーでも、一番端へ動かした場合に発生することがあります）
</details>

### 1-3. Node-REDで実行

<!-- [![Image from Gyazo](https://i.gyazo.com/b88f34195bd6883cc732431f49f13c6f.gif)](https://gyazo.com/b88f34195bd6883cc732431f49f13c6f) -->

以下のソースコードを読み込み、初期化処理コードを設定して動かしてみましょう。
obnizスイッチを押したとき、左に倒したとき、右に倒したとき、でサーボモーターが動くことを確認してください。
ノードの中身は各自で確認してみてください。

```json
[{"id":"fd4d9924.ded5e8","type":"obniz-repeat","z":"d9dba4a1.01f228","obniz":"","name":"","interval":"100","code":"msg.payload = await obniz.switch.getWait();\n\nreturn msg;","x":350,"y":320,"wires":[["d2cf9b4d.518638","49f8bacd.ab65e4"]]},{"id":"d2cf9b4d.518638","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"let degrees = context.get('degrees')||90; // 角度を保持する変数（無ければ初期化）\r\n\r\nobniz.display.clear(); // 画面を消去\r\n\r\nif (msg.payload === 'push') {\r\n // スイッチが押されている状態\r\n degrees = 45.0;\r\n} else if (msg.payload === 'right') {\r\n // 右にスイッチを倒したとき\r\n degrees = 0.0;\r\n} else if (msg.payload === 'left') {\r\n // 左にスイッチを倒したとき\r\n degrees = 180.0;\r\n} else {\r\n // スイッチが押されていない状態\r\n degrees = 90.0;\r\n}\r\ncontext.set('degrees',degrees);//現在の角度をコンテキストへ保存\r\n\r\n// ディスプレイに角度を表示\r\nobniz.display.print(`Current: ${degrees} deg`);\r\n// サーボを指定の角度まで動かす\r\nobnizParts.servo.angle(degrees);","x":560,"y":320,"wires":[[]]},{"id":"49f8bacd.ab65e4","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":550,"y":380,"wires":[]}]
```

▼初期化処理コード
```json
obnizParts.servo = obniz.wired("ServoMotor",{ gnd:0, vcc:1, signal:2 });
```

<details>
<summary>heavy output. output voltage is too low when driving highが発生する場合</summary>

[![Image from Gyazo](https://i.gyazo.com/c0c2cc772af37003785f5eb812225a09.png)](https://gyazo.com/c0c2cc772af37003785f5eb812225a09)
Node.jsでもこのような過電流警告が出ます。`Ctrl+C`でいったん終了させてから再度実行してみましょう。
</details>

