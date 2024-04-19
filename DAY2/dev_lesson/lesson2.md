# 生成AIに仕事を手伝わせたりサービスに組み込んだりしてみよう

ChatGPTのリリースを皮切りに生成AIへの熱が高まり、後続でさまざまな生成AIやチャットボットツールや、生成AIを簡単に使えるツールがリリースされています。

（ちなみに、この資料も「Cursor」という、生成AIによりプログラミングや文章作成を手伝ってくれるエディターを使って作成しています。）


生成AIと仲良くなって、楽に・楽しく・自分の可能性を広げましょう！


## 目標
ChatGPTをはじめとした複数のAIチャットボットツールをつかって文章や、Node-REDのフローを生成する


## やってみよう

### いくつかの生成AIチャットボットツールを使ってみよう


話題の生成AIチャットボットツール

| サービス名 | 説明 | 特徴 | 備考 | URL |
| ------------ | ---- | ---- | ---- | ---- |
| ChatGPT      | OpenAI | 自然な文章生成が得意 | Microsoftが多額の出資 | https://chat.openai.com/ |
| Gemini       | Google | 豊富なデータを活用 | - | https://gemini.google.com/ |
| Claude       | Anthropic |  | OpenAI元幹部らが独立した会社。Amazon
やGoogleが出資。GPT-4上回るLLM（Large Language Model）と話題に | https://claude.ai/chats |


馴染みのAIチャットボットツールを使いつつ、用途によりほかのツールを使い分けできるととても便利です。


それぞれの出力の違いやUIの違いを体験してみてください。



今回は、3つの生成AIチャットボットツールを使い簡単に作文してみましょう！



#### やってみよう

「お題：1日目の授業の感想を400字で書かせ、Teamsに投稿する。」

入れて欲しい内容
- 楽しかったこと
- 辛かったこと
- 学び

文章のトーン
ブログ風、報告書風、小説風など好きなトーンでOKです。



ChatGPT、Gemini、Claudeそれぞれ、どのような出力になるか比較してみましょう。


<details><summary>🌟 生成AIがうまく使えない？**「プロンプト」の書き方**が、結果を大きく左右します。</summary>

生成AIへの指示文章のことを「プロンプト」といいます。
[参考](https://japan.zdnet.com/article/35203152/)
これらのポイントを意識してプロンプトを作成することで、生成AIの出力結果を向上させることができます。

</details>


<details><summary>1. ChatGPTのはじめかた</summary>

<img src="https://i.gyazo.com/3cc7c8546ab22e97bda58692093b0445.png" width="500px">
[![Image from Gyazo](https://i.gyazo.com/3cc7c8546ab22e97bda58692093b0445.png)](https://gyazo.com/3cc7c8546ab22e97bda58692093b0445)

1. 初めてログインする場合は「Sign up」、すでにアカウントがある場合は「Log in」をクリックします。（どちらの場合も似たようなログイン画面へ遷移します）ここでは、初めてログインする場合の「Sign up」から進めます.

<img src="https://i.gyazo.com/60929dc4220fc48b8caa60056f7529b6.png" width="500px">
[![Image from Gyazo](https://i.gyazo.com/60929dc4220fc48b8caa60056f7529b6.png)](https://gyazo.com/60929dc4220fc48b8caa60056f7529b6)

2. `Continue with Google` をクリックすると、現在利用中のGoogleアカウントを選択できる画面になるので、どれか1つをクリックしてそのGoogleアカウントでサインインします.

<img src="https://i.gyazo.com/a4a25a2eeda215e21b548a9772901be9.png" width="500px">
[![Image from Gyazo](https://i.gyazo.com/a4a25a2eeda215e21b548a9772901be9.png)](https://gyazo.com/a4a25a2eeda215e21b548a9772901be9)

3. 名前と生年月日を入力します。生年月日は「月/日/西暦年」の順であることに注意してください.

<img src="https://i.gyazo.com/f81fbdf77f1275e7500f848ff41ec350.png" width="500px">
[![Image from Gyazo](https://i.gyazo.com/f81fbdf77f1275e7500f848ff41ec350.png)](https://gyazo.com/f81fbdf77f1275e7500f848ff41ec350)

4. アカウントの不正取得防止のため、携帯電話番号を入力して認証する必要があります。6桁の番号が書かれたSMSが送られてくるので、次の画面でその番号を入力してください.

<img src="https://i.gyazo.com/488890ea14e6993c9485b03af36568f1.png" width="500px">
[![Image from Gyazo](https://i.gyazo.com/488890ea14e6993c9485b03af36568f1.png)](https://gyazo.com/488890ea14e6993c9485b03af36568f1)

5. 認証が成功すると、次のような画面になってアカウント作成は完了です。何かダイアログが出てくる場合、「Next」や「Done」をクリックして進めてしまえば閉じることができます。

</details>


<details><summary>2. Geminiのはじめかた</summary>
1. [Gemini](https://gemini.google.com/?hl=ja)にアクセスし、「ログイン」をクリック。
<img src="https://i.gyazo.com/319ba04e43fe1e7ff5545846b276aced.jpg" width="500px">

2. Googleのアカウントでログイン、または、アカウントを作成します。
<img src="https://i.gyazo.com/3614e0ac5fb2ec5b4c92b9fdd670515b.png" width="500px">

3. ログイン後、「Geminiとはなそう」をクリック
<img src="https://i.gyazo.com/22db8342e81fbb85f3b67b3e42e33af3.jpg" width="500px">

4. これで準備は完了です！
<img src="https://i.gyazo.com/0bfe5aea5bbb6f23c3e621fc26c19ba6.png" width="500px">

🌟 下記のようなエラーが出た場合、個人アカウントを使うようにしてください。
<img src="https://i.gyazo.com/945abf04370923525705f824d38141b5.png" width="500px">


</details>



<details>
  <summary>3. Claudeのはじめかた</summary>

1. [Claude](https://claude.ai/chats)にアクセスし、ログインまたはサインアップ（新規アカウント作成）を行います。

  <div style="display: flex; flex-wrap: wrap;">
    <figure>
      <img src="https://i.gyazo.com/f2f1c01855cf5f6958167b8ae37175f9.png" width="400px" alt="Image 1">
      <figcaption>2. ログインすると、名前を聞かれますので答えてください。</figcaption>
    </figure>
    <figure>
      <img src="https://i.gyazo.com/746b9eb1e0d442ef63c54260a59fdd4a.png" width="400px" alt="Image 2">
      <figcaption>3. 注意事項に目を通し「Sounds Good, Let's Begin」をクリックするとスタートします。</figcaption>
    </figure>
  </div>
</details>



### 生成AIにNode-REDのフローを書いてもらい、インポートする


生成AIはコーディングもできます。

Node-REDにインポートできる形式で、Node-REDのフローをかいてもらうという使い方ができます。


1. OpenAIのアカウントを作成
[ChatGPT](https://chat.openai.com/)を開き、アカウントを作成してください。すでに持っている方はあるもので構いません。

2. プロンプトを書き、ChatGPT/Gemini/Claudeのいずれかにフローを生成してもらう

```

以下のように動作するNode-REDのフローJSONを出力してください

- 3つのInjectノードではじまる。それぞれのノードは、payloadにりんご・みかん・バナナと入力。
- 3つのInjectノードからswitchにつなぐ。
    - りんごの場合: 赤を出力
    - みかんの場合: オレンジを出力
    - バナナの場合: 黄色を出力
- debugノードにレスポンスを表示する


```

3. 出力をインポートする
Node-REDのインポート機能で、出力されたJSONデータを貼り付けし、インポートしてください。

<img src="https://i.gyazo.com/899837fd64bfcfb1b23cd574edbf4775.png" width="500px" alt="Image 3">


## まとめ

ChatGPTをはじめとした複数のAIチャットボットツールを使って
文章を作成したり、フローをかいたりできるようになりました！

