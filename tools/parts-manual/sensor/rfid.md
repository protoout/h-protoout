# マニュアル: RFID（MFRC522）

電波を用いてICタグの情報を非接触で読み書きする自動認識技術です。

使われている事例: 
- [ユニクロの「レジ待ち行列」を解消したRFIDタグの威力](https://agenda-note.com/retail/detail/id=1294)

**★ 極性(+ -)があるため、接続に間違いがないか注意**

## 1. obnizでの配線

## 2. 使うノードとつなぎ方


## 3. 各ノードの設定方法


```javascript

obnizParts.mrfc522 = obniz.wired("MFRC522", { cs: 0, clk: 1, mosi: 2, miso: 3, gnd: 5, rst: 6});

```