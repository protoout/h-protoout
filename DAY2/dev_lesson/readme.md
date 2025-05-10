
# 生成 AI の活用と IoT

## 授業ガイダンス

### 1. 本日の授業でやること・ゴール  

> やること:
> - **AI を使って、プロトタイピングを企画・制作する**
> - **最終制作のアイデアを整理する**
>   
> ゴール:
> - **制作の幅を広げ、自身のアイデアをカタチにする流れを明確にする**

### 2. タイムテーブル 
  前半は実装、後半は最終制作のためのアイデアワークをします！前回学んだ内容も扱います。
    
  | 時間        | 内容                                       |
  |-------------|--------------------------------------------|
  | 09:00-09:15 | 授業ガイダンス |
  | 09:15-10:30 | Lesson01 生成AIの活用 | 
  | 10:30-11:00 | Lesson02 API 連携をしてみよう | 
  | 11:00-12:00 | Lesson03 AI 技術を取り入れて制作してみよう | 
  | 12:00-13:00 | 昼食 | 
  | 13:00-14:15 | Lesson04 IoTプロトタイプを作ってみよう |
  | 14:15-14:30 | 休憩 | 
  | 14:30-17:00 | アイデアワーク | 

### 3. 授業の進め方

#### ■[使うツール](../../DAY1/dev_lesson/lesson00-overview/00_tools.md)  
前回のDay1と同じですが、一応揃っているか確認しましょう。  
アイデアワークで **Miro** と **SharePoint** というツールを使います。
  
#### ■[授業の進め方を紹介します](../../DAY1/dev_lesson/lesson00-overview/01_overview.md)  
こちらも前回と同じです。　　
質問がある時は、[GitHub Discussions](https://github.com/protoout/h-protoout/discussions) を活用しましょう。

----  

## Lesson01 生成AIの活用  

> やること:
> - **生成AI に触れる**
> - **Node-RED 開発に生成 AI を活用する**
>   
> ゴール:
> - **生成 AI とやりとりをしてフローの改善ができるようになる**

> [!WARNING]
> ここからは ChatGPT の話題にも触れますが、授業中の制作に関しては Day1 同様、 Effibot 使って進めていきます。  
 
### コラム

#### 生成AI概論と生成AIに触れてみる
- [1-1. 生成AIコラム](https://www.canva.com/design/DAGmxHLZuOQ/aUtN16EzZWLMJqkfsn7HCA/edit)
- [1-2. GPT-4oを体験してみよう](./lesson01-generative-ai/01_2_gpt4o-touch.md)
- [1-3. 生成AI（LLM）を使ってみる](./lesson01-generative-ai/01_3_start-llm.md)

### ハンズオンの準備

obniz Board と Node-RED の2つを使える状態にします。  
- [obniz Board を Wi-Fi 接続する](../../DAY1/dev_lesson/lesson00-overview/02_env_obniz.md)
- [GitHub CodeSpaces から Node-RED を立ち上げる](../../DAY1/dev_lesson/lesson00-overview/03_env_nodered.md)  

生成 AI が Node-RED 用のコードを上手くつくるためのプロンプト例を用意しました。(適宜使用する箇所にリンクを用意しています)
- [プロンプトサンプル](../../tools/prompt-sample.md)

### 実装

#### 1-1. 生成AIとプログラムを書いてみる Node-RED 開発ハンズオン
- [1-1-1. 生成AIを使ってNode-REDの処理を書いてみる](./lesson01-generative-ai/02_1_make-node-red-flow.md)
- [1-1-2. 生成AI使ってNode-REDの処理をさらに書いてみる](./lesson01-generative-ai/02_2_update-node-red-flow.md)
- [1-1-3. センサーを繋いでみる](./lesson01-generative-ai/02_3_sensor.md)



####  1-2. 応用課題： 生成AIでフローを0から作って改善してみるハンズオン
- [1-2-1. 0から生成AIで作ってみる](./lesson01-generative-ai/03_1_zero1.md)
- [1-2-2. 生成AIが作ったフローを改修](./lesson01-generative-ai/03_2_one2.md)

####  1-3. 応用課題： 生成AIが作ったフローの改修やデバッグ
- [1-3-1. 既存のJSONを読み込んでスタート](./lesson01-generative-ai/04_1_ten99.md)

----  

## Lesson02 API 連携をしてみよう

> やること:
> - **外部のサービスやAPIを連携する**
>
> ゴール:
> - **既存のサービスや API を利用して自分のやりたいことを達成する感覚を掴む**

### 実装

#### 2-1. [Teams API を連携して obniz Board から通知してみよう](./lesson02-api/01_teams.md)
#### 2-2. [その他の外部 API を使ってみよう](./lesson02-api/02_nasa.md)


参考： [様々な API 活用事例紹介](./lesson02-api/03_api-use-case.md)

----  

## Lesson03 AI 技術を取り入れて制作してみよう

> やること:
> - **各自が興味のあるハンズオンを選んで実施**
>   
> ゴール: 
> - **各自自身の興味のあるコンテンツを進めて応用イメージを膨らます**

### 実装

AIハンズオンのどれかをやってみましょう
  
#### 3-1. [生成 AI のノードを利用してみよう：テキストを解析し翻訳する](./lesson03-handson/A-1_openai-node-gtp.md)
           
#### 3-2. [生成 AI  のノードを利用してみよう：画像を解析しLEDを操作する](./lesson03-handson/A-2_openai-node-wisper.md)
           
#### 3-3. [Teachable Machine を使って画像分析モデルをつくろう](./lesson03-handson/A-3_teachable-machine.md)

----  

## Lesson04 IoT プロトタイプを作ってみよう

> やること:
> - **学んだことを使ってアイデアを形にする**
>   
> ゴール: 
> - **他の資料やハンズオンの内容を改造して自分のアイデア実現に使う感覚をつかむ**

### ■[テーマと進め方について](./lesson04-prototyping/01_prototyping.md)


----

実装パートは以上となります。

このあとは最終制作に向けたアイデアソンになります。

ここまでお疲れ様でした。

**[◀ 目次ページに戻る](./readme.md)**

----  

