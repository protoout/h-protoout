# マニュアル: DCモーター

サーボモータは角度付きですがDCモーターは回転しつづけます。

> <img src="https://docs.obniz.com/ja/sdk/parts/DCMotor/image.jpg" width="50">

> 出典：[obniz公式ライブラリ](https://docs.obniz.com/ja/sdk/parts/DCMotor/README.md)

ピンのアサインと実際の配線は、みなさんがやりたいことに合わせて適宜変更をしてください。

## 1. obnizでの配線

**★ 極性(+ -)はありますが、逆に接続すると回転の向きが変わる仕様なので危険度は少ないです。**

<details><summary>配線の仕方をクリックで開く</summary>
<img src="https://docs.obniz.com/ja/sdk/parts/DCMotor/wired.png" alt="Image from Gyazo" width="500"/>

二本出ている線のどちらをつけても大丈夫です。逆に付けると回転の向きが逆になります。

- forward: 0番ピン
- back: 1番ピン

</details>

## 2. 使うノードとつなぎ方

`Injectノード`と`obniz functionノード`を接続します。

## 3. 各ノードの設定方法

- obniz functionのコード

```javascript
obnizParts.motor.forward();
```

- obniz functionのコード（止める場合）

```javascript
obnizParts.motor.stop();
```

## 4. 初期化処理コードの編集

```javascript
obnizParts.motor = obniz.wired("DCMotor", {forward:0, back:1});
```

5. 結果

Injectノードを押すとモーターが回転します。

> <img src="" width="400px" />

■ 参考資料
[obnizの公式ドキュメント: DCモーター](https://docs.obniz.com/ja/sdk/parts/DCMotor/README.md)

</details>