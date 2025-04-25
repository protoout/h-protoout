
## 生成 AI の活用と IoT

### 生成 AI を武器にしよう

#### 1. 本日の授業でやること・ゴール  

> [!NOTE]
> やること:
> - AI を使って、プロトタイピングを企画・制作する
> - 最終制作のアイデアを整理する
>   
> ゴール:
> - 制作の可能性を広げ、自身のアイデアをカタチにする流れを明確にする

#### 2. タイムテーブル 
  前半は実装、後半は最終制作のためのアイデアワークをします！前回学んだ内容も扱います。
    
  | 時間        | 内容                                       |
  |-------------|--------------------------------------------|
  | 09:00-09:15 | 生成 AI を武器にしよう |
  | 09:15-10:30 | Lesson01 生成AIの活用 | 
  | 10:30-11:00 | Lesson02 API 連携をしてみよう | 
  | 11:00-12:00 | Lesson03 AI 技術を取り入れて制作してみよう | 
  | 12:00-13:00 | 昼食 | 
  | 13:00-14:15 | Lesson04 IoTプロトタイプを作ってみよう |
  | 14:15-14:30 | 休憩 | 
  | 14:30-17:00 | アイデアワーク | 

#### 3. 環境構築 

使うものはDay1と同じです。

obniz Board と Node-RED の2つを使える状態にします。  
1. [obniz Board を Wi-Fi 接続する](./lesson00-overview/02_env.md) 
2. [GitHub CodeSpaces から Node-RED を立ち上げる](./lesson00-overview/02_env.md)

その他、使うツールを紹介します。  
- [電子部品とアプリケーション](./lesson00-overview/00_tools.md)
  
Day1で扱った電子部品の使い方はこちらにまとまっています。
- [電子部品を obniz Board と Node-RED で扱う](https://zenn.dev/protoout/books/07_node-red-obniz)

----  

### Lesson01 生成AIの活用  

> [!NOTE]
> やること:
> - 生成AI に触れる
> - Node-RED 開発に生成 AI を活用する
> ゴール:
> - 生成AIとやりとりをしてフローの改善ができるようになる

#### 実装

> [!IMPORTANT]
> この授業では"Effibot"という謹製の生成 AI サービスを使います。
> ※注意点

1. 生成AI概論と生成AIに触れてみる
    - [1-1. 生成AIコラム](./lesson01-generative-ai/01_1_overview.md)
    - [1-2. GPT-4oを体験してみよう](./lesson01-generative-ai/01_2_gpt4o-touch.md)
    - [1-3. 生成AI（LLM）を使ってみる](./lesson01-generative-ai/01_3_start-llm.md)

2. 生成AIとプログラムを書いてみる Node-RED 開発ハンズオン
    - [2-1. 生成AIを使ってNode-REDの処理を書いてみる](./lesson01-generative-ai/02_1_make-node-red-flow.md)
    - [2-2. 生成AI使ってNode-REDの処理をさらに書いてみる](./lesson01-generative-ai/02_2_update-node-red-flow.md)
    - [2-3. センサーを繋いでみる](./lesson01-generative-ai/02_3_sensor.md)

3. 生成AIでフローを0から作って改善してみるハンズオン
    - [3-1. 0から生成AIで作ってみる](./lesson01-generative-ai/03_1_zero1.md)（時間があれば実施）
    - [3-2. 生成AIが作ったフローを改修](./lesson01-generative-ai/03_2_one2.md)（時間があれば実施）

4. 生成AIが作ったフローの改修やデバッグ
    - [4-1. 既存のJSONを読み込んでスタート](./lesson01-generative-ai/04_1_ten99.md)（時間があれば実施）

----  

### Lesson02 API 連携をしてみよう

> [!NOTE]
> やること:
> - 外部のサービスやAPIを連携する
>
> ゴール:
> - 既存のサービスやAPIを利用して自分のやりたいことを達成する感覚を掴む 

#### 実装

1. [Teams API連携](./lesson02-api/01_teams.md)
2. [その他のAPI](./lesson02-api/02_nasa.md)
3. [API活用事例紹介](./lesson02-api/03_api-use-case.md)

----  

### Lesson03 AI 技術を取り入れて制作してみよう

> [!NOTE]
> やること:
> - 各自が興味のあるハンズオンを選んで実施
>   
> ゴール: 
> - 各自自身の興味のあるコンテンツを進めて応用イメージを膨らます

#### 実装

[Lesson03の進め方と各ハンズオンの紹介](./lesson03-handson/readme.md)

### 3-1. まずはAIハンズオンのどれかをやってみましょう

- A-1. [OpenAIのノードをつかってみよう simple gtpノードでAPIから取得したデータを翻訳](./lesson03-handson/A-1_openai-node-gtp.md)
- A-2. [OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する](./lesson03-handson/A-2_openai-node-wisper.md)
- A-3. [Teachable Machineの利用](./lesson03-handson/A-3_teachable-machine.md)


----  

### Lesson04 IoT プロトタイプを作ってみよう

> [!NOTE]
> やること:
> - 学んだことを使ってアイデアを形にする
>   
> ゴール: 
> - 他の資料やハンズオンの内容を改造して自分のアイデア実現に使う感覚をつかむ

#### 実装

[作ってみよう](./lesson04-prototyping/01_prototyping.md)



----

実装パートは以上となります。

このあとは最終制作に向けたアイデアソンになります。

ここまでお疲れ様でした。

**[◀ 目次ページに戻る](./readme.md)**

----  

1. [今日の授業の進め方](./day2-overview.md)
2. [Node-RED環境について](./env.md)
3. [新しいobnizのWi-Fi設定について](./obniz-wifi.md)
4. よく使う資料をまとめました
    - [制作に役立つ道具集ページ](../../tools/)
        - [パーツマニュアル](../../tools/parts-manual)
5. [DAY2の演習中に待ち時間があったら進めてほしいこと](../day2-sukima.md)
6. DAY1の振り返りなど

- A-4. [GPT-4oを使ってアプリケーション開発](./lesson03-handson/A-4_gpt4o.md)


### 3-3. おまけ。さらに時間がある人でAIをさらに使ってみたい人

ただしC群のハンズオンは環境的にやれない人がいるかもしれないのであくまでもおまけコンテンツです。
- C-1. [SunoAIを使って初めての作詞作曲](https://note.com/n0bisuke/n/n0f1d5a2a6c8f)
    - ChatGPTとSunoAIで作詞作曲をしてみましょう。
- C-2. [GPTsでオリジナルChatGPTを作成](https://zenn.dev/n0bisuke/books/gpts-handson-book/viewer/1-2_what-is-gpt)
    - GPTsというオリジナルChatGPTを作れる機能のハンズオンです。
    - 今までは有償機能でしたが、5/13のリリースで無料ユーザーにも解放されたらしいです。（無料の人は使うだけらしいけど、ユーザーによってまだ解放されてないかもしれません。）
