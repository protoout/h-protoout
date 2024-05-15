# マニュアル: RFID（MFRC522）

電波を用いてICタグの情報を非接触で読み書きする自動認識技術です。

使われている事例: 
- [ユニクロの「レジ待ち行列」を解消したRFIDタグの威力](https://agenda-note.com/retail/detail/id=1294)

**★ 極性(+ -)があるため、接続に間違いがないか注意**

## 1. obnizでの配線

<details><summary>配線の仕方をクリックで開く</summary>

<a href="https://gyazo.com/6f793dd18a2eef8afb7d9f68a643ea0a"><img src="https://i.gyazo.com/6f793dd18a2eef8afb7d9f68a643ea0a.jpg" alt="Image from Gyazo" width="500"/></a>

| 電子パーツの脚         | obnizピン         | obniz pin settings         |
|--------------|---------------|---------------|
|  SDA |  obnizの0番    | cs    |
|  SCK  |   obnizの1番   | clk    |
|  MOSI  |   obnizの2番   | mosi     |
|  MISO  |   obnizの3番   | miso    |
|  IRQ |   obnizの4番   | -    |
|  GND  |   obnizの5番   | gnd    |
|  RST  |   obnizの6番   | rst    |
|  3.3V  |   obnizの7番   | vcc    |

</details>

## 2. 使うノードとつなぎ方

<details><summary>ノードの繋ぎ方をクリックで開く</summary>
- obniz repeat
- dedbug

<a href="https://gyazo.com/f12a5b25d4c360c7e545ededed17019e"><img src="https://i.gyazo.com/f12a5b25d4c360c7e545ededed17019e.png" alt="Image from Gyazo" width="520"/></a>

</details>


## 3. 各ノードの設定方法


- obniz repeat

コードを書き換える

```javascript

let uid;

let card = await obnizParts.mrfc522.findCardWait();
uid = "UID        : " + card.uid;

msg.payload = uid;


return msg;

```


## 4. 初期化コードの編集

```javascript

obnizParts.mrfc522 = obniz.wired("MFRC522", { cs: 0, clk: 1, mosi: 2, miso: 3, gnd: 5, rst: 6}); 

```

## 4. 結果

下記のような挙動になればOKです。

- RFIDを検出できないとき：Error: card_search_ERRORが出る
- RFIDを検出したとき：UIDが表示される

<a href="https://gyazo.com/e8eab5066df60e923f4d720864fe07dd"><img src="https://i.gyazo.com/e8eab5066df60e923f4d720864fe07dd.png" alt="Image from Gyazo" width="428"/></a>