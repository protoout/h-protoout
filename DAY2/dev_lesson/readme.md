# Day2 生成AIを知るではなく使ってプロトタイピング

本日の実装授業では、前回学んだことも使いながら外部サービスとの連携や生成AI活用をおこなっていきます。

## ■ [授業における肖像権・著作権の取り扱いについて](https://protoout.notion.site/acde308ffe03498fad30a271b4a7b128?pvs=4)
## ■ [注意と今日の流れ](./lesson00-info.md)

## まずはじめに 【8:55〜9:10】

1. [今日の授業の進め方](./day2-overview.md)
2. [Node-RED環境について](./env.md)
3. よく使う資料をまとめました
    - [制作に役立つ道具集ページ](../../tools/)
        - [パーツマニュアル](../../tools/parts-manual)
4. [DAY2の演習中に待ち時間があったら進めてほしいこと](./day2-sukima.md)
5. DAY1の振り返りなど

## Lesson01 生成AIの活用 【9:10〜10:30】 担当: のびすけ

- **やること: ChatGPTに触れる、Node-REDのフローを生成する**
- **ゴール: 生成AIとやりとりをしてフローの改善ができるように**

1. 生成AIに触れる
    - [生成AIを使ってみる](./lesson01-generative-ai/01_1_overview.md)
    - [世界最速! GPT-4oを体験してみよう](./lesson01-generative-ai/01_2_gpt4o-touch.md)
    - [生成AIを使ってみる](./lesson01-generative-ai/01_3_start-llm.md)
2. 生成AIとプログラムを書いてみるNode-RED開発ハンズオン
    - [2-1. 生成AIを使ってNode-REDの処理を書いてみる](./lesson01-generative-ai/02_1_make-node-red-flow.md)
    - [2-2. 生成AI使ってNode-REDの処理をさらに書いてみる](./lesson01-generative-ai/02_2_update-node-red-flow.md)
    - [2-3. センサーを繋いでみる](./lesson01-generative-ai/02_3_sensor.md)
3. 生成AIでフローを0から作って改善してみるハンズオン
    - [3-1. 0から生成AIで作ってみる](./lesson01-generative-ai/03_1_zero1.md)
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
- A-2. [OpenAIのノードをつかってみよう wisperを使って、音声でLEDを操作する](./lesson03-handson/a_openai-node-wisper.md)
- A-3. [Teachable Machineの利用](./lesson03-handson/c_teachable-machine.md)
- A-4. [GPT-4oを使ってアプリケーション開発](./lesson03-handson/A-4_gpt4o.md)

### 3-2. 時間がある人はNode-REDとセンサーを組み合わせたハンズオンのどれかをやってみましょう

- B-1. [チュートリアル1]()
- B-2. [チュートリアル1]()
- B-3. [チュートリアル1]()
- B-4. [チュートリアル1]()

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

