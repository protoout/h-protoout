# ダッシュボードにデータの表示・操作を行おう

## 目標
GUI（画面で操作できるユーザーインタフェース）にセンサーの値を表示したり、操作したりできるようになる。

## 完成イメージ

`@flowfuse/node-red-dashboard`を使い、GUI（画面で操作できるユーザーインタフェース）を作ってみましょう。

## やってみよう

1. 外部ノードを追加。`@flowfuse/node-red-dashboard`をインストール

<img src="https://i.gyazo.com/3239a2d14644f8ceabb85272b301fd0a.png" width="500">

<img src="https://i.gyazo.com/5406ef2554c6e2b63397d03a8f886090.png" width="500">

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
msg.payload = await obnizParts.hcsr04.measureWait();

obniz.display.clear(); // クリア
obniz.display.print('Ready');

// 距離を取得
let distance = msg.payload;
// そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい
distance = Math.floor(distance);

// 距離(mm)をデバッグに表示
msg.payload = (distance + ' mm');
// obnizディスプレイに表示
// 一度消してから距離+mmの単位を表示
obniz.display.clear();
obniz.display.print(distance + ' mm');

// 距離がある程度未満かどうかの判定
if (distance < 50) { // 50mm = 5cm 以下の場合
    // obnizディスプレイに近接していることを表示
    obniz.display.clear();
    obniz.display.print('Too close!!');
}

return msg;

```

4. obniz初期化コードを修正

```Javascript
obnizParts.hcsr04 = obniz.wired("HC-SR04", { gnd: 0, echo: 1, trigger: 2, vcc: 3 });

```

5. gaugeノードを編集
<img src="https://i.gyazo.com/091adee22b51586b23cc069b52f2c933.png" alt="Image Description" width="500">


6. デプロイして、ダッシュボードを開く

<img src="https://i.gyazo.com/90ee96555fd28491f8df7e0e4cadfef0.png" alt="Image Description" width="500">

<img src="https://i.gyazo.com/ef074f17d4ccd08ecdf17baa0e02800b.png" alt="Image Description" width="500">

<img src="https://i.gyazo.com/2fa2740dfc1285cf1a57c5efc468e0ca.gif" alt="Image Description" width="500">



### 完成したフロー

```JSON
[
    {
        "id": "dda95691c8ab3ced",
        "type": "debug",
        "z": "35131428dc29ef13",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 630,
        "y": 140,
        "wires": []
    },
    {
        "id": "eae6eb14b4f274ea",
        "type": "obniz-function",
        "z": "35131428dc29ef13",
        "obniz": "a1e02a9aa2adf951",
        "name": "",
        "code": "msg.payload = \"close\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;",
        "x": 420,
        "y": 140,
        "wires": [
            [
                "dda95691c8ab3ced"
            ]
        ]
    },
    {
        "id": "b12a3a54eac0d2b3",
        "type": "inject",
        "z": "35131428dc29ef13",
        "name": "",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 240,
        "y": 140,
        "wires": [
            [
                "eae6eb14b4f274ea"
            ]
        ]
    },
    {
        "id": "e42d3d96.12046",
        "type": "obniz-repeat",
        "z": "35131428dc29ef13",
        "obniz": "a1e02a9aa2adf951",
        "name": "",
        "interval": "1000",
        "code": "msg.payload = await obnizParts.hcsr04.measureWait();\n\n// 距離を取得\nlet distance = msg.payload;\n// そのままだと小数点以下の桁数がやたら多いので整数に丸めてもよい\ndistance = Math.floor(distance);\n\n// 距離(mm)をデバッグに表示\nmsg.payload = (distance + ' mm');\n// obnizディスプレイに表示\n// 一度消してから距離+mmの単位を表示\nobniz.display.clear();\nobniz.display.print(distance + ' mm');\n\n// 距離がある程度未満かどうかの判定\nif (distance < 50) { // 50mm = 5cm 以下の場合\n    // obnizディスプレイに近接していることを表示\n    obniz.display.clear();\n    obniz.display.print('Too close!!');\n}\n\nreturn msg;",
        "x": 230,
        "y": 280,
        "wires": [
            [
                "402408dd.31b188",
                "0ca654b2a0720711"
            ]
        ]
    },
    {
        "id": "402408dd.31b188",
        "type": "debug",
        "z": "35131428dc29ef13",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 510,
        "y": 280,
        "wires": []
    },
    {
        "id": "0ca654b2a0720711",
        "type": "ui_gauge",
        "z": "35131428dc29ef13",
        "name": "",
        "group": "4a03c246.55f3d8",
        "order": 0,
        "width": 0,
        "height": 0,
        "gtype": "gage",
        "title": "",
        "label": "units",
        "format": "{{value}}",
        "min": 0,
        "max": "2000",
        "colors": [
            "#00b500",
            "#e6e600",
            "#ca3838"
        ],
        "seg1": "",
        "seg2": "",
        "diff": false,
        "className": "",
        "x": 490,
        "y": 360,
        "wires": []
    },
    {
        "id": "a1e02a9aa2adf951",
        "type": "obniz",
        "obnizId": "40725365",
        "deviceType": "obnizboard1y",
        "name": "キサイチ",
        "accessToken": "LU9lVJcNb47aDtOxRk5pPlPCxeiA5ServT8g20LtCOeeEtM2mmgcgqNUglK9gvvo",
        "code": "obnizParts.hcsr04 = obniz.wired(\"HC-SR04\", { gnd: 0, echo: 1, trigger: 2, vcc: 3 });"
    },
    {
        "id": "4a03c246.55f3d8",
        "type": "ui_group",
        "name": "Default",
        "tab": "ccec3682.947098",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false
    },
    {
        "id": "ccec3682.947098",
        "type": "ui_tab",
        "name": "Home",
        "icon": "dashboard",
        "order": 1
    }
]

```



---

**[◀ 目次ページに戻る](../readme.md)**