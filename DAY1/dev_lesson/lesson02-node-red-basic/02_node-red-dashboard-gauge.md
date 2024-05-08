# ダッシュボードにデータの表示・操作を行おう

## 目標
GUI（画面で操作できるユーザーインタフェース）にセンサーの値を表示したり、操作したりできるようになる。

## 完成イメージ

`@flowfuse/node-red-dashboard`を使い、GUI（画面で操作できるユーザーインタフェース）を作ってみましょう。

## やってみよう

1. 外部ノードを追加。`@flowfuse/node-red-dashboard`をインストール

<img src="https://i.gyazo.com/3239a2d14644f8ceabb85272b301fd0a.png" width="500">

<a href="https://gyazo.com/31991f40b40e79c2c4b26317b9544867"><img src="https://i.gyazo.com/31991f40b40e79c2c4b26317b9544867.png" alt="Image from Gyazo" width="500"/></a>

2. 3つのノードを配置し、下記のようにつなぐ
- obniz repeatノード
- gaugeノード
- debgノード

<img src="https://i.gyazo.com/fea27422b28852f9a9cc0ad484ab780a.png" alt="Image Description" width="500">

3. obniz repeatノードを設定

<img src="https://i.gyazo.com/9a7660d0a55108ea8cf99ad6c41f7afa.png" alt="Image Description" width="500" >
- interval(ms) 1000
- コード

```javascript

let distance = await obnizParts.hcsr04.measureWait();

msg.payload = Math.round(distance); //小数点以下四捨五入

return msg;

```

4. obniz初期化コードを修正

```Javascript
obnizParts.hcsr04 = obniz.wired("HC-SR04", { gnd: 0, echo: 1, trigger: 2, vcc: 3 });

```

5. gaugeノードを編集

<a href="https://gyazo.com/ac305d335cd76b0017278587d161267d"><img src="https://i.gyazo.com/ac305d335cd76b0017278587d161267d.png" alt="Image from Gyazo" width="500"/></a>


6. デプロイして、ダッシュボードを開く

<a href="https://gyazo.com/7e6ce9752c9be286085f8afe02af8418"><img src="https://i.gyazo.com/7e6ce9752c9be286085f8afe02af8418.png" alt="Image from Gyazo" width="500"/></a>

<a href="https://gyazo.com/751162ab9518b881c16a8018b63eda92"><img src="https://i.gyazo.com/751162ab9518b881c16a8018b63eda92.png" alt="Image from Gyazo" width="500"/></a>


この様に表示されていれば成功です！

<a href="https://gyazo.com/425c81e869007055ab5a7ab983d0e2c2"><img src="https://i.gyazo.com/425c81e869007055ab5a7ab983d0e2c2.gif" alt="Image from Gyazo" width="396"/></a>



### 完成したフロー

```JSON

[{"id":"e42d3d96.12046","type":"obniz-repeat","z":"35131428dc29ef13","obniz":"","name":"","interval":"1000","code":"let distance = await obnizParts.hcsr04.measureWait();\n\nmsg.payload = Math.round(distance); //小数点以下四捨五入\n\nreturn msg;","x":250,"y":360,"wires":[["86b535098be9c481"]]},{"id":"86b535098be9c481","type":"ui-gauge","z":"35131428dc29ef13","name":"距離センサーの値表示","group":"87cd8706e6ac0dbc","order":0,"width":3,"height":3,"gtype":"gauge-half","gstyle":"needle","title":"gauge","units":"units","icon":"","prefix":"","suffix":"","segments":[{"from":"0","color":"#5cd65c"},{"from":"800","color":"#ffc800"},{"from":"1500","color":"#ea5353"}],"min":0,"max":"2000","sizeThickness":16,"sizeGap":4,"sizeKeyThickness":8,"styleRounded":true,"styleGlow":false,"className":"","x":520,"y":340,"wires":[]},{"id":"87cd8706e6ac0dbc","type":"ui-group","name":"My Group","page":"da3dfdd988e3076c","width":6,"height":1,"order":-1,"showTitle":true,"className":"","visible":true,"disabled":false},{"id":"da3dfdd988e3076c","type":"ui-page","name":"Page N","ui":"465c930a4d633284","path":"/pageN","icon":"home","layout":"grid","theme":"25bee87fb63ed474","order":-1,"className":"","visible":"true","disabled":"false"},{"id":"465c930a4d633284","type":"ui-base","name":"My Dashboard","path":"/dashboard","includeClientData":true,"acceptsClientConfig":["ui-notification","ui-control"],"showPathInSidebar":false,"navigationStyle":"default"},{"id":"25bee87fb63ed474","type":"ui-theme","name":"Default Theme","colors":{"surface":"#ffffff","primary":"#0094CE","bgPage":"#eeeeee","groupBg":"#ffffff","groupOutline":"#cccccc"},"sizes":{"pagePadding":"12px","groupGap":"12px","groupBorderRadius":"4px","widgetGap":"12px"}}]

```



---

**[◀ 目次ページに戻る](../readme.md)**