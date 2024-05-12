# マニュアル: パトランプ

**★ 極性(+ -)があるため、接続に間違いがないか注意**

<img src="https://ueeshop.ly200-cdn.com/u_file/UPAH/UPAH808/2108/products/14/69524b4790.jpg?x-oss-process=image/format,webp" width="50">, 出典：[Keyestudio](https://www.keyestudio.com/products/keyestudio-traffic-light-module-black-and-eco-friendly-for-arduino)

<details><summary>使い方をクリックで開く</summary>
1. obnizでの配線

<a href="https://gyazo.com/8464f2e5de5bac0515ec7b4cea9d4b96"><img src="https://i.gyazo.com/8464f2e5de5bac0515ec7b4cea9d4b96.jpg" alt="Image from Gyazo" width="500"/></a>

| 電子パーツの脚         | obnizピン         |
|--------------|---------------|
| GND  |  obnizの3番    |
|  G  |   obnizの4番   |
|  Y  |   obnizの5番   |
|  R  |   obnizの6番   |

2. 使うノードとつなぎ方
- injection
- obniz function
- debug

<a href="https://gyazo.com/4f52c51092088a407d00b64e5c347a12"><img src="https://i.gyazo.com/4f52c51092088a407d00b64e5c347a12.png" alt="Image from Gyazo" width="500"/></a>

3. 各ノードの設定方法

- injection

<a href="https://gyazo.com/ed7b5fc7363878099a5f6cf42314aae5"><img src="https://i.gyazo.com/ed7b5fc7363878099a5f6cf42314aae5.gif" alt="Image from Gyazo" width="500"/></a>


- obniz function

```javascript

obnizParts.light.single(msg.payload); //payloadの文字列がredなら赤、yellowなら黄色、greenなら緑で光らせる

return msg;


```


4. 初期化処理コードの編集

3番、4番、5番、6番に接続する例です。

```javascript

obnizParts.light = obniz.wired("Keyestudio_TrafficLight", {gnd:3, green:4, yellow:5, red:6});


```


5. 結果

injectionノードのボタンをクリックすると、赤いLEDが光ります。

injectionノードでpayloadの設定を「green」「yellow」に変更すると、違う色のLEDが光ります。


■ 参考資料
[obnizの公式ドキュメント: Keyestudio TrafficLight](https://docs.obniz.com/ja/sdk/parts/Keyestudio_TrafficLight/README.md)

</details>