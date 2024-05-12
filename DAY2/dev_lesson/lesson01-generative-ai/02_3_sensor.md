# L01-生成AI: 生成AIと一緒にNode-REDでIoT開発 3/3

引き続きやっていきます。ここではいよいよセンサーに接続してみます。

## 3. 距離センサーが反応したら音を出す

### 3-1. 距離センサーとスピーカーの配線

**ここからはセンサーは貸し合って試してみてください。**

写真のように配線してみましょう。

<img src="https://i.gyazo.com/53bb7be7ba1d99ed2934715654e4b1f3.png" width="400px" />

- 0,1,2,3ピンに超音波距離センサー
- 9,11ピンにスピーカー

を繋げてみます。

### 3-1. 距離センサーに差し替え

エミュレートで使っていた`injectノード`,`changeノード`を`obniz repeatノード`に差し替えましょう。

<img src="https://i.gyazo.com/d4fb9397dff4fbfcf93c7f26d5da1117.png" width="400px" />


### 3-

こんな感じでステップを踏んでフローを変えてきたイメージがなんとなく掴めていると嬉しいです。

> <img src="https://i.gyazo.com/fbdcafe1eacd1e10bb644d620ab35a4a.png" width="400px" />


**[◀ 目次ページに戻る](../readme.md)**