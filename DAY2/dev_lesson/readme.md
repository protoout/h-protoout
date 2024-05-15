# Day2 知るだけでなく、生成AIを使ってプロトタイピング

本日の実装授業では、前回学んだことも使いながら外部サービスとの連携や生成AI活用をおこなっていきます。

## ■ [授業における肖像権・著作権の取り扱いについて](https://protoout.notion.site/acde308ffe03498fad30a271b4a7b128?pvs=4)
## ■ [【🚨怪我しないでね👀】センサーやアクチュエーターを扱う際の諸注意](https://protoout.notion.site/c7dfd3de1aa94e9c8403ee94c8bbcdf2?pvs=4)

## まずはじめに 【8:55〜9:10】

1. [今日の授業の進め方](./day2-overview.md)
2. [Node-RED環境について](./env.md)
3. [新しいobnizのWi-Fi設定について](./obniz-wifi.md)
4. よく使う資料をまとめました
    - [制作に役立つ道具集ページ](../../tools/)
        - [パーツマニュアル](../../tools/parts-manual)
5. [DAY2の演習中に待ち時間があったら進めてほしいこと](../day2-sukima.md)
6. DAY1の振り返りなど

## Lesson01 生成AIの活用 【9:10〜10:30】 担当: のびすけ

- **やること: ChatGPTに触れる、Node-RED開発にChatGPTを活用する**
- **ゴール: 生成AIとやりとりをしてフローの改善ができるように**

1. 生成AI概論と生成AIに触れてみる
    - [1-1. 生成AIコラム](./lesson01-generative-ai/01_1_overview.md)
    - [1-2. 世界最速! GPT-4oを体験してみよう](./lesson01-generative-ai/01_2_gpt4o-touch.md)
    - [1-3. 生成AI（LLM）を使ってみる](./lesson01-generative-ai/01_3_start-llm.md)

2. 生成AIとプログラムを書いてみるNode-RED開発ハンズオン
    - [2-1. 生成AIを使ってNode-REDの処理を書いてみる](./lesson01-generative-ai/02_1_make-node-red-flow.md)
    - [2-2. 生成AI使ってNode-REDの処理をさらに書いてみる](./lesson01-generative-ai/02_2_update-node-red-flow.md)
    - [2-3. センサーを繋いでみる](./lesson01-generative-ai/02_3_sensor.md)

3. 生成AIでフローを0から作って改善してみるハンズオン
    - [3-1. 0から生成AIで作ってみる](./lesson01-generative-ai/03_1_zero1.md)（時間があれば実施）
    - [3-2. 生成AIが作ったフローを改修](./lesson01-generative-ai/03_2_one2.md)（時間があれば実施）

4. 生成AIが作ったフローの改修やデバッグ
    - [4-1. 既存のJSONを読み込んでスタート](./lesson01-generative-ai/04_1_ten99.md)（時間があれば実施）

## Lesson02 API・外部サービス連携でさらに広げていこう 【10:30〜11:00】 担当:私市

- **やること:外部のサービスやAPIを連携する** 
- **ゴール:既存のサービスやAPIを利用して自分のやりたいことを達成する感覚を掴む** 

1. [Teams API連携](./lesson02-api/01_teams.md)
2. [その他のAPI](./lesson02-api/02_nasa.md)
3. API活用事例紹介

## Lesson03 選択してAI利用のハンズオンをやってみよう 【11:00〜12:00 / 13:00~14:00】 担当: 私市, のびすけ 

- **やること: 各自が興味のあるハンズオンを選んで実施**
- **ゴール: 各自自身の興味のあるコンテンツを進めて応用イメージを膨らます** 

[Lesson03の進め方と各ハンズオンの紹介](./lesson03-handson/readme.md)

### 3-1. まずはAIハンズオンのどれかをやってみましょう

A-1~4のどれかのハンズオンを優先的に実施してください。

- A-1. [OpenAIのノードをつかってみよう simple gtpノードでAPIから取得したデータを翻訳](./lesson03-handson/A-1_openai-node-gtp.md)
- A-2. [OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する](./lesson03-handson/A-2_openai-node-wisper.md)
- A-3. [Teachable Machineの利用](./lesson03-handson/A-3_teachable-machine.md)
- A-4. [GPT-4oを使ってアプリケーション開発](./lesson03-handson/A-4_gpt4o.md)

### 3-2. 時間がある人はNode-REDとセンサーを組み合わせたハンズオンのどれかをやってみましょう

- B-1. [チュートリアル1: 温湿度センサーを使用し、熱中症アラートを作ろう](/tools/tutorials/01_temp_led.md)
- B-2. [チュートリアル2: サーボモーターとCdSで明るくなったら90度、暗くなったら0度になるものをつくろう](/tools/tutorials/02_servo_cds.md)
- B-3. [チュートリアル3: サーボモーターでピョコピョコ連続で動かす](/tools/tutorials/03_servo-pyokopyoko.md)

### 3-3. おまけ。さらに時間がある人でAIをさらに使ってみたい人

ただしC群のハンズオンは環境的にやれない人がいるかもしれないのであくまでもおまけコンテンツです。
- C-1. [SunoAIを使って初めての作詞作曲](https://note.com/n0bisuke/n/n0f1d5a2a6c8f)
    - ChatGPTとSunoAIで作詞作曲をしてみましょう。
- C-2. [GPTsでオリジナルChatGPTを作成](https://zenn.dev/n0bisuke/books/gpts-handson-book/viewer/1-2_what-is-gpt)
    - GPTsというオリジナルChatGPTを作れる機能のハンズオンです。
    - 今までは有償機能でしたが、5/13のリリースで無料ユーザーにも解放されたらしいです。（無料の人は使うだけらしいけど、ユーザーによってまだ解放されてないかもしれません。）

## Lesson04 プロトタイピングとふりかえり 14:00~14:30

**やること:** 
**ゴール:** 

- 1. [作ってみよう](./lesson04-prototyping/01_prototyping.md)
- 2. 実装パートまとめと明日に向けて

---

実装パートは以上となります。

このあとは最終制作に向けたアイデアソンになります。

ここまでお疲れ様でした。

**[◀ 目次ページに戻る](./readme.md)**


