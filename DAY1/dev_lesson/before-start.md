
### **新しいことをはじめる前に**  

1つページが終わり次のことをはじめる前に、下記3つの手順をかならず行うようにしてください

**1. タブの無効化**

以降の作業でノードを読み込む前に、今まで作業していたNode-REDの**タブを無効化**し、有効なタブは必ず常に1つのみにしてください。
ノードが混在すると分かりづらくなりobnizが予期せぬ動作をすることがあります。

<img src="https://i.gyazo.com/48f43c4c3ea95f30a4569f382490cc05.png" width="500">

**2. タブの新規作成**
1. 「+」をクリック
<a href="https://gyazo.com/6a6d96fec786b923f70512e1de4b3551"><img src="https://i.gyazo.com/6a6d96fec786b923f70512e1de4b3551.png" alt="Image from Gyazo" width="500"/></a>

2. 新しくできたタブをダブルクリックし、名前をわかりやすく変更する。
<a href="https://gyazo.com/9392ad19397802dbfb49f53550cc48f5"><img src="https://i.gyazo.com/9392ad19397802dbfb49f53550cc48f5.png" alt="Image from Gyazo" width="500"/></a>

**3. 停止用フローの読み込み**
1. 下記のコードをすべてコピーしてください。

```json
[{"id":"cb1d6d3a.017e1","type":"debug","z":"d9dba4a1.01f228","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":610,"y":140,"wires":[]},{"id":"11a346f0.5a4c19","type":"obniz-function","z":"d9dba4a1.01f228","obniz":"","name":"","code":"msg.payload = \"close\";\nawait obniz.wait(1000); \nobniz.close();\n\nreturn msg;","x":440,"y":140,"wires":[["cb1d6d3a.017e1"]]},{"id":"76e43759.3dff68","type":"inject","z":"d9dba4a1.01f228","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":260,"y":140,"wires":[["11a346f0.5a4c19"]]}]
```

Node-REDの右上のメニュー（三本線）から読み込みを選びます。

<a href="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c"><img src="https://gyazo.com/5db5478433b4918912ee79ae9e3e515c.png" alt="Image from Gyazo" width="372"/></a>

      

コピーしたコードを貼り付けます  
<a href="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a"><img src="https://gyazo.com/dcf7feebd57ec66ac012304ee4838e4a.png" alt="Image from Gyazo" width="372"/></a>
