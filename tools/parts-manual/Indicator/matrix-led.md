# マニュアル: マトリクスLED

8x8のマトリクスLEDです（`Keyestudio_HT16K33`）

<img src="https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/image.jpg" width="50">

> 出典：[obniz公式ライブラリ](https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/README.md)

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。

## 1. obnizでの配線

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<details><summary>配線の仕方をクリックで開く</summary>
<img src="https://i.gyazo.com/13ab90f80705f099b43fdf75766033ed.png" alt="Image from Gyazo" width="500"/>

左から写真の向きで

- vcc: 0番ピン
- gnd: 1番ピン
- sda: 2番ピン
- scl: 3番ピン

</details>

## 2. 使うノードとつなぎ方

`Injectノード`と`obniz functionノード`を接続します。

## 3. 各ノードの設定方法

- obniz functionのコード

```javascript
const dots = [1,2,4,8,16,32,64,128]
matrix.dots(dots);
```

## 4. 初期化処理コードの編集

```javascript

obnizParts.matrix = obniz.wired("Keyestudio_HT16K33", { vcc:0, gnd:1, sda:2, scl:3 });

```

5. 結果

Injectノードを押すとマトリクスLEDが斜めに光ります。

> <img src="https://i.gyazo.com/15da82b6277ebfdf68597b229ccaeb23.jpg" width="400px" />

■ 参考資料
[obnizの公式ドキュメント: マトリクスLED](https://docs.obniz.com/ja/sdk/parts/Keyestudio_HT16K33/README.md)

</details>