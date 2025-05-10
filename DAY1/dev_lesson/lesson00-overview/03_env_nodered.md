# Node-REDの準備
GitHub から Node-RED の環境をつくっていきます。以下の手順で進めましょう。

1. GitHub CodeSpaces のタイムアウトの時間設定
2. GitHub CodeSpaces を起動し、Node-RED を立ち上げる

> [!Note]
> Day2は上記 2. から始めます
> [こちらの URL](https://github.com/codespaces) からスタートできます。必要な時にまたご案内します。

## GitHub CodeSpaces のタイムアウトの時間設定[^1]  

### ■[こちらを別タブで開いて GitHub CodeSpaces タイムアウトを設定ましょう](https://github.com/settings/codespaces#:~:text=browser%20with%20JupyterLab.-,Default%20idle%20timeout,-A%20codespace%20will)
  
最大値である **240 minutes** に設定して保存(Save)しましょう。 
> <a href="https://gyazo.com/18451c2331a371bb7b3d941ef15fb6e7"><img src="https://i.gyazo.com/18451c2331a371bb7b3d941ef15fb6e7.png" alt="Image from Gyazo" width="600"/></a>

> [!NOTE]
> GitHub CodeSpaces は GitHub が提供するクラウド上の開発環境です。[^2]
> この環境を連続で使い続けられる時間が最大で240分ということです。
> 一度タイムアウトしても、またすぐに接続することができます。

このリンク先での作業は終了です。別タブで開いた設定ページを閉じてください。

[^1]: [タイムアウトの設定方法](https://docs.github.com/ja/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces#setting-your-default-timeout-period)
[^2]: [GitHub CodeSpaces について](https://github.co.jp/features/codespaces)

----

## GitHub リポジトリから GitHub CodeSpaces を立ち上げましょう

GitHub 上に Node-Red を立ち上げるためのプログラムを事前に用意しました。
以下のリンクから GitHub CodeSpaces を立ち上げましょう。

### ■[こちらを別タブで開いて GitHub リポジトリにアクセスしましょう](https://github.com/protoout/github-codespces-node-red)  
  
こちらのプロジェクト上で `Code` > `Codespaces` > `Create codespaces on main` と進んでいくと、別のタブが立ち上がります。
  
> <a href="https://gyazo.com/1e7e8baa8a64bcef71715e4b759cf319"><img src="https://i.gyazo.com/1e7e8baa8a64bcef71715e4b759cf319.png" alt="Image from Gyazo" width="600"/></a>
  
画像のように、画面の右下の部分(ターミナル)でプログラムが自動で実行されますので2，3分ほど待ちましょう。  
  
> <a href="https://gyazo.com/ec96d281003445960ee2d1c35d87abe6"><img src="https://i.gyazo.com/ec96d281003445960ee2d1c35d87abe6.png" alt="Image from Gyazo" width="600"/></a>
>   
> 実は、プロジェクトファイルにはこのような処理を実行するための指示が書かれています  
  
 しばらくするとターミナルの最後に `Started flow` と表示されます。これで Node-RED の準備ができました。
>
> <a href="https://gyazo.com/de1962b15da3db3aaba1b001eb575a46"><img src="https://i.gyazo.com/de1962b15da3db3aaba1b001eb575a46.png" alt="Image from Gyazo" width="600"/></a>


----  
  
## 最後のステップです。Node-RED にアクセスしましょう

`ポート`タブを開くとポート1880という行に1つのプロセスが実行されています。  
表示範囲を`Private` > `Public` に変更し、提供されているリンクをブラウザで開いてみましょう。 

> 表示範囲は、プロセスのある位置(例えば `🔓Private` と書いてあるところ)で右クリックすると設定できます。
> <a href="https://gyazo.com/1b6b3b191a268e9413e51e4dabf617e6"><img src="https://i.gyazo.com/1b6b3b191a268e9413e51e4dabf617e6.png" alt="Image from Gyazo" width="600"/></a>   


 丸いインターネットのマークをクリックするか、リンクをコピーして別のタブで開けばOKです
>   
> <a href="https://gyazo.com/8312bd0793c1501800cfadad74ee75f9"><img src="https://i.gyazo.com/8312bd0793c1501800cfadad74ee75f9.png" alt="Image from Gyazo" width="600"/></a>
>   
> `https://XXXX-XXXX-XXXXXX-1880.app.github.dev/` のようなURLです。

  
このような Node-RED の画面が立ち上がれば準備完了です！プロジェクト機能に関する案内は `後にする` を選んで閉じてしまいましょう。

<a href="https://gyazo.com/bf8177b07618ad1cd7a79556bc5630ca"><img src="https://i.gyazo.com/bf8177b07618ad1cd7a79556bc5630ca.png" alt="Image from Gyazo" width="600"/></a>

ここまで、お疲れさまでした！
  
---

**[◀ 目次ページに戻る](../readme.md)**


