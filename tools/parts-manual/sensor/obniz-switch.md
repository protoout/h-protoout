# マニュアル: obnizのスイッチ


## 1. 使うノードとつなぎ方

<details><summary>ノードの繋ぎ方をクリックで開く</summary>

- obniz repeat
- debug

<a href="https://gyazo.com/487d1ea101c3f910198c6ca3a1dd431d"><img src="https://i.gyazo.com/487d1ea101c3f910198c6ca3a1dd431d.png" alt="Image from Gyazo" width="300"/></a>

</details>

## 2. 各ノードの設定方法

- obniz repeat

```javascript

msg.payload = await obniz.switch.getWait(); //msg.payloadにobnizのスイッチの状態を格納

return msg; //msg.payloadを出力

```


## 3. 結果

コンソールにスイッチの状態が出力されるのを確認してください。

- 押していないとき: none
- 押したとき: push
- 右に倒したとき: right
- 左に倒したとき: left

■ 参考資料
[obnizの公式ドキュメント: スイッチ](https://docs.obniz.com/ja/reference/common/switch)

