
## IoT の世界に飛び込もう！obniz と Node-RED で手を動かして学ぶ IoT

### IoT の世界へようこそ
    
#### 1. 本日の授業でやること・ゴール  

> やること:
> - **IoTデバイスを簡単に開発・制御できるデバイス( obniz Board )を使って、プロトタイピングを企画・制作する**
>   
> ゴール:
> - **アイデアをカタチにする楽しさを感じつつ、自分の手でつくる感覚を身に着ける**
  
  
#### 2. タイムテーブル  
  
  1日中制作をします！はじめから実際に手を動かしていきます！
    
  | 時間        | 内容                                       |
  |-------------|--------------------------------------------|
  | 10:00-10:20 | IoTの世界へようこそ |
  | 10:20-11:00 | Lesson01 obnizをはじめよう | 
  | 11:00-12:00 | Lesson02 いろいろな電子部品を触ってみよう | 
  | 12:00-13:00 | 昼食 | 
  | 13:00-14:30 | Lesson03 実用的なセンサーをつくってみよう |
  | 14:30-14:50 | 休憩 | 
  | 14:50-16:30 | Lesson04 IoT プロトタイプを作ってみよう | 
  | 16:30-17:00 | 最終制作に向けて | 

    
#### 3. 環境構築  

obniz Board と Node-RED の2つを使える状態にします。  
1. [obniz Board を Wi-Fi 接続する](./lesson00-overview/02_env.md) 
2. [GitHub CodeSpaces から Node-RED を立ち上げる](./lesson00-overview/02_env.md)

その他、使うツールを紹介します。  
- [電子部品とアプリケーション](./lesson00-overview/00_tools.md)
    
----  
  
### Lesson01 obniz をはじめよう

> やること:  
> - **ハードウェアの第一歩、「Lチカ」をやってみる**
> 
> ゴール:  
> - **授業のペースに乗って、手を動かして実働させる体験をする**
>

#### 実装  
  
1. [obnizをはじめよう](./lesson01-obniz-basic/01_start_obniz.md)
2. [Lチカしてみよう](./lesson01-obniz-basic/02_obniz-LED.md)

早く終わった人はこちらに挑戦！
- つけたLEDが10秒後に消えるようにしてみよう

----  


### Lesson02 いろいろな電子部品を触ってみよう  

> やること:  
> - **さらにたくさんの電子パーツを試す**
>  
> ゴール:  
> - **授業資料を見ながら、様々な電子部品を動かせるようになる**

#### 実装

ここからは参考資料を見ながら自分で進めてみましょう！  
  
リンクは[こちら](https://zenn.dev/protoout/books/07_node-red-obniz)です。実装テーマごとにリンクを用意しています。  

![image](https://github.com/user-attachments/assets/59e201e2-5e46-40d9-b636-a346c9818f46)

1. [ブザーで好きな音を出してみよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-speaker)
2. [サーボモーターを回してみよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-servo)

> [!WARNING]
> 注意！サーボモータが動かないことがあります。[^1]  
> obniz Board (1Yではなく)では電源の電流がリークし、obniz Board が過電流[^2]を検知し電源を供給できない場合があります。
> 過電流を検知すると obniz Board に次のようなメッセージが表示されます。
> ```
> output voltage is too low when driving high. io state has changed output to input
> ```
> <details>
> <summary>その場合は、こちらの対策を試してみてください</summary>
>   
>   **1. ブレッドボードにつなぐ**  
>   繋ぎ方の画像を入れる  
>     
>   **2. 電圧を指定する**  
>   初期化のコードに `voltage:"3v"` のオプションを入れます。コードにすると、次の通りです。
> ```
> obnizParts.servo = obniz.wired("ServoMotor", {gnd:0,vcc:1,signal:2,voltage:"3v"});
> ```    
> </details>

[^1]: [obniz Boardの過電流検知により電源を供給できない場合](https://docs.obniz.com/ja/sdk/parts/ServoMotor/README.md#:~:text=%E9%9B%BB%E6%BA%90%E3%82%82obniz%20Board%E3%81%AB%E7%B9%8B%E3%81%92%E3%82%89%E3%82%8C%E3%82%8B%E3%83%A2%E3%83%BC%E3%82%BF%E3%83%BC%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
[^2]: [過電流検知](https://docs.obniz.com/ja/reference/common/io/output#:~:text=%E5%88%A9%E7%94%A8%E3%81%97%E3%81%BE%E3%81%99%E3%80%82-,%E9%81%8E%E9%9B%BB%E6%B5%81%E6%A4%9C%E7%9F%A5,-obniz%20board%E3%81%AA%E3%81%A9)

早く終わった人はこちらに挑戦！
- [ブザーで曲を奏でてみよう](https://gist.github.com/ma1750/df348ecc867703467a91ac74f3b61d8e)
- [サーボモーターを時計回りに120度逆回りに60度回してみよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/turorial-servo-keep-moving)
> [!CAUTION]
> ブザーの方、曲探す
  
----  
### 休憩

----  

### Lesson03 実用的なセンサーをつくってみよう  

> やること:  
> - **電子部品を組み合わせて、世の中にあるセンサを再現する**
> 
> ゴール:  
> - **世の中にあるセンサーがどのような仕組みで動くのか、イメージできるようになる**

#### 実装  
  
1. 距離に応じてライトの色を変えてみよう：感知式信号機  
    - [2つのセンサを組み合わせる方法]()
> [!CAUTION]
> zennチュートリアル。ノードも必要なので、1番目だけ資料つくる
    
2. 周りが暗くなったらLEDを点灯させる仕組みをつくってみよう：スマホの明るさの自動調整    
    - [照度センサー](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-cds)
    - [LED](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/tutorial-led-onoff)  
  
3. 湿度が低くなったら警告音を出してみよう：熱中症計  
    - [温湿度センサー](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-temp-hum-dht20)
    - [ブザー](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-speaker)

早く終わった人はこちらに挑戦！
- 温度に応じてサーボーモーターの回転方向を変えてみよう：シーリングファン



----  
### 休憩

----  

### Lesson04 IoT プロトタイプを作ってみよう

> やること:
> - **今日学んだことをフル活用して、アイデアを形にする**
> 
> ゴール:
> - **企画と技術の両面を見て簡単なプロダクトに落とし込む**

これまで学んだことを使ってプロトタイプを作ってみましょう
テーマは[こちら](./lesson04-prototyping.md)

> [!CAUTION]
> ↑余裕あったらネタ考える

----  

### Lesson05 最終制作に向けて

最終発表のテーマと準備についてお知らせします。  
  
リンクは[こちら](./lesson05-closing.md)
  
----  

**[◀ 目次ページに戻る](./readme.md)**



----  

> [!CAUTION]
> 以下、念のため非難させてる↓

![image](https://github.com/user-attachments/assets/00139787-1a36-456f-8423-ecae8688c26b)

### その他参考資料

- [obnizで複数のパーツを同時に使うときのTips](./obniz-tips.md): 制作に役立つ複数のパーツを同時に使うときのTips
- [新しいことをはじめる前に](./before-start.md): 新しいことをはじめるまえに必ず行う手順をまとめた資料

### Lesson02 Node-REDの基本的な考え方と操作を学ぼう【13:40〜14:30】

**やること:** Node-REDの基礎とフローの作り方を学ぶ

**ゴール:** コピペでなく意図をもってアイデアをプログラムに落とす感覚を掴む

1. [よくつかわれる「コアノード」を学ぼう](./lesson02-node-red-basic/01_node-red-corenode.md)
2. [ダッシュボードにデータの表示・操作を行おう「gauge」](./lesson02-node-red-basic/02_node-red-dashboard-gauge.md)
2. [ダッシュボードにデータの表示・操作を行おう「chart」](./lesson02-node-red-basic/03_node-red-dashboard-chart.md)


### Lesson03 もっといろいろな電子部品を触ってみよう【14:45〜15:15】

**やること:** さらにたくさんの電子パーツを試す

**ゴール:** Lesson01、02で学んだことをつかって新しいことを学ぶ・試す感覚を掴む

3. [スピーカーで音を鳴らしてみよう](./lesson01-obniz-basic/03_obniz-speaker.md)
4. [超音波測距センサーで距離を取得しよう](./lesson01-obniz-basic/04_obniz-distance.md)
1. [サーボモーター](./lesson03-obniz-advanced/01_obniz-servo.md)
2. [照度センサー（CdS）](./lesson03-obniz-advanced/02_obniz-cds.md)
3. [温湿度センサー](./lesson03-obniz-advanced/03_obniz-temp.md)
4. [LED信号モジュール](./lesson03-obniz-advanced/04_obniz-ledlights.md)
