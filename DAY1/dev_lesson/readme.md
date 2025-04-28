# IoT の世界に飛び込もう！obniz と Node-RED で手を動かして学ぶ IoT

## 授業ガイダンス
    
### 1. 本日の授業でやること・ゴール  

> やること:
> - **IoTデバイスを簡単に開発・制御できるデバイス( obniz Board )を使って、プロトタイピングを企画・制作する**
>   
> ゴール:
> - **アイデアをカタチにする楽しさを感じつつ、自分の手でつくる感覚を身に着ける**
  


### 2. タイムテーブル  
  
  1日中制作をします！はじめから実際に手を動かしていきます！
    
  | 時間        | 内容                                       |
  |-------------|--------------------------------------------|
  | 10:00-10:20 | 授業ガイダンス |
  | 10:20-11:00 | Lesson01 obnizをはじめよう | 
  | 11:00-12:00 | Lesson02 いろいろな電子部品を触ってみよう | 
  | 12:00-13:00 | 昼食 | 
  | 13:00-14:30 | Lesson03 実用的なセンサーをつくってみよう |
  | 14:30-14:50 | 休憩 | 
  | 14:50-16:30 | Lesson04 IoT プロトタイプを作ってみよう | 
  | 16:30-17:00 | 最終制作に向けて | 
  
  
### 3. 授業の進め方

#### ■[使うツール](./lesson00-overview/00_tools.md)  
  
#### ■[授業の進め方を紹介します](./lesson00-overview/01_overview.md)  
  
----  
  
## Lesson01 obniz をはじめよう

> やること:  
> - **ハードウェアの第一歩、「Lチカ」をやってみる**
> 
> ゴール:  
> - **授業のペースに乗って、手を動かして実働させる体験をする**
>

### ハンズオンの準備

obniz Board と Node-RED の2つを使える状態にします。  
- [obniz Board を Wi-Fi 接続する](./lesson00-overview/02_env_obniz.md)
- [GitHub CodeSpaces から Node-RED を立ち上げる](./lesson00-overview/03_env_nodered.md)  
   
### 実装  
  
#### 1-1. [obnizをはじめよう](./lesson01-obniz-basic/01_start_obniz.md)
#### 1-2. [Lチカしてみよう](./lesson01-obniz-basic/02_obniz-LED.md)
  
早く終わった人はこちらの課題にも挑戦！  
  
#### 1-3. 応用課題：LED を点けて5秒後に消えるようにしてみよう
- [ヒント](https://github.com/protoout/h-protoout/blob/main/DAY1/dev_lesson/lesson01-obniz-basic/02_obniz-LED.md#:~:text=%E3%81%BF%E3%81%BE%E3%81%97%E3%82%87%E3%81%86%EF%BC%81-,4%2D3.%20%E5%8D%98%E7%B4%94%E3%81%AA%E7%82%B9%E6%BB%85,-obniz%2Dfunction%E3%83%8E%E3%83%BC%E3%83%89)  

----  


## Lesson02 いろいろな電子部品を触ってみよう  

> やること:  
> - **さらにたくさんの電子パーツを試す**
>  
> ゴール:  
> - **授業資料を見ながら、自分の力で様々な電子部品を動かす**

### 実装

#### 2-1. [ブザーでドレミの音を出してみよう](./lesson01-obniz-basic/03_obniz-speaker.md)

**ここからは参考資料を見ながら自分で進めてみましょう！**  
  
参考資料：[**obniz x Node-REDマニュアル**](https://zenn.dev/protoout/books/07_node-red-obniz)  
> ※以降の実装テーマには、この資料の中から必要なページをリンクさせています  
>![image](https://github.com/user-attachments/assets/59e201e2-5e46-40d9-b636-a346c9818f46)

#### 2-2. [サーボモーターを回してみよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/actuator-servo)

> [!TIP]
> 注意！サーボモータが動かないことがあります。[^1]  
> obniz Board (1Y ではなく)ではサーボモーターの電源の電流がリークし、obniz Board が過電流[^2]を検知し電源を供給できない場合があります。
> 過電流を検知すると obniz Board に次のようなメッセージが表示されます。
> ```
> output voltage is too low when driving high. io state has changed output to input
> ```

<details>
<summary>もしこのようなメッセージが表示されるときは、こちらの対策を試してください</summary>

1. 現在の実行状態を `obniz close` で停止させる  

2. ブレッドボードにつなぐ  
繋ぎ方の画像を入れる  
 
3. 電圧を指定する  
初期化のコードに `voltage:"3v"` のオプションを入れます。コードにすると、次の通りです。
```
obnizParts.servo = obniz.wired("ServoMotor", {gnd:0,vcc:1,signal:2,voltage:"3v"});
```    
</details>

早く終わった人はこちらの課題にも挑戦！  

#### 2-3. 応用課題：ブザーで曲を奏でよう
- [ヒント](./lesson02-node-red-basic/practice_speaker_song.md)   
#### 2-4. 応用課題：サーボモーターを30度と90度を繰り返し行き来させよう  
- [ヒント](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/turorial-servo-keep-moving)  
  
----  
### 休憩

----  

## Lesson03 実用的なセンサーをつくってみよう  

> やること:  
> - **電子部品を組み合わせて、世の中にあるセンサーを再現する**
> 
> ゴール:  
> - **世の中にあるセンサ技術を再現し、自身の制作の幅を広げる**

### 実装  

**ここでは複数の電子部品を組み合わせてみます。  
一気に活用の幅が増え、世の中で使われているセンサーも簡易的に再現することができます！**  


#### 3-1. 感知式信号機[^3]  
- [距離に応じてライトの色を変えてみよう](./lesson03-obniz-advanced/combine_trafficlight_ultrasound.md)
  
> <img width="400" alt="image" src="https://github.com/user-attachments/assets/36f6f62e-ea25-4130-98ed-38a856dce850" />
>   
> 車があまり通らない場所では、車がいることを超音波センサで感知してから信号機のライトを制御する仕組みになっています。  
> 停止線より手前で止まりすぎると信号が変わらないということも...  
    
#### 3-2. ソーラーパネルの自動追尾[^4]  

- [明るさによってサーボーモーターの動きを変えよう](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/tutorial-servo-cds)
  
> <img width="400" alt="image" src="https://github.com/user-attachments/assets/ac7b4f5c-0997-47ca-af70-f8e419bcc3ff" />
>    
> ソーラーパネルは効率的に太陽光エネルギーを回収するために照度に合わせてパネルの角度を変える仕組みになっていると言われています。
> その他にも、スマートブラインド[^5]などにも同様の仕組みが使われています。
　　
早く終わった人はこちらの課題にも挑戦！ 
  
#### 3-3. 応用課題： 熱中症予防[^6]  

- 気温が高さに応じて、警戒レベルをLEDの光で表そう
> <img width="400" alt="image" src="https://github.com/user-attachments/assets/934a87cb-f7bb-4bbe-9ad1-f0f08536a3cc" />
>   
> デジタル温湿度計にはこのような温湿度センサーが搭載されています。  
> なお、本格的な熱中症計は、太陽の陽ざしや地面からの照り返しなどの輻射熱を測るために、黒球と呼ばれる黒い球で温度を測っています[^6]
- ヒント
    - [温湿度計のノードの設定](https://zenn.dev/protoout/books/07_node-red-obniz/viewer/sensor-temp-hum-dht20)
> [!CAUTION]
> zenn記事リンク切れあり
 
  
#### 3-4. 応用課題：「3-3. 熱中症計」にインフルエンザのリスクをブザーで知らせる機能を追加しよう  
  
- ヒント
    - インフルエンザのリスクの計算式について、生成 AI で調べてみましょう
    - 「3-3.」のノードを JSON で書きだして生成 AI で編集してもらおう


----  
### 休憩

----  

## Lesson04 IoT プロトタイプを作ってみよう

> やること:
> - **今日学んだことをフル活用して、アイデアを形にする**
> 
> ゴール:
> - **企画と技術の両面を見て簡単なプロダクトに落とし込む**

これまで学んだことを使ってプロトタイプを作ってみましょう！  

### ■[テーマと進め方について](./lesson04-prototyping.md)

----  

## Lesson05 最終制作に向けて

### ■[最終発表のテーマと準備について](./lesson05-closing.md)  
  
  
----  

**[◀ 目次ページに戻る](./readme.md)**

[^1]: [obniz Boardの過電流検知により電源を供給できない場合](https://docs.obniz.com/ja/sdk/parts/ServoMotor/README.md#:~:text=%E9%9B%BB%E6%BA%90%E3%82%82obniz%20Board%E3%81%AB%E7%B9%8B%E3%81%92%E3%82%89%E3%82%8C%E3%82%8B%E3%83%A2%E3%83%BC%E3%82%BF%E3%83%BC%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)

[^2]: [過電流検知](https://docs.obniz.com/ja/reference/common/io/output#:~:text=%E5%88%A9%E7%94%A8%E3%81%97%E3%81%BE%E3%81%99%E3%80%82-,%E9%81%8E%E9%9B%BB%E6%B5%81%E6%A4%9C%E7%9F%A5,-obniz%20board%E3%81%AA%E3%81%A9)

[^3]: [感知式信号機の仕組み](https://www.shinshu-komagane.com/word/responsible_traffic_signal/#:~:text=%E4%BA%A4%E9%80%9A%E9%87%8F%E3%81%AE%E5%B0%91%E3%81%AA%E3%81%84%E9%81%93%E8%B7%AF,%E3%81%8C%E9%9D%92%E3%81%AB%E5%A4%89%E3%82%8F%E3%82%8B%E4%BB%95%E7%B5%84%E3%81%BF%E3%80%82%EF%BC%89&text=%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8,%E6%9C%80%E5%B0%8F%E9%99%90%E3%81%AB%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82)

[^4]: [ソーラーパネルの自動追尾機能](https://www.nextracker.com/)
  
[^5]: [Switch BotのIoTブラインド](https://prtimes.jp/main/html/rd/p/000000036.000057002.html)

[^6]: [熱中症の危険度がわかる温湿度計](https://www.plus-vision.com/jp/product/eisei/onshitsudo-ledalerm.html)

[^7]: [黒球式熱中アラーム](https://www.tanita.co.jp/magazine/special-feature/5322/)
  
----  
