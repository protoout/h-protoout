# Node-REDの準備
GitHub から Node-RED の環境をつくっていきます。以下の手順で進めましょう。

1. GitHub CodeSpaces のタイムアウトの時間設定
2. GitHub リポジトリをフォークする
3. GitHub CodeSpaces を起動し、Node-RED を立ち上げる]

> [!Note]
> Day2は上記 3. から始めます

## GitHub CodeSpaces のタイムアウトの時間設定[^1]  

### ■[こちらから GitHub CodeSpaces タイムアウトを設定ましょう](https://github.com/settings/codespaces#:~:text=browser%20with%20JupyterLab.-,Default%20idle%20timeout,-A%20codespace%20will)
  
最大値である **240 minutes** に設定して保存(Save)しましょう。 
> ![image](https://github.com/user-attachments/assets/28c1fa44-6bf3-4656-8f88-b8877150340e)

> [!NOTE]
> GitHub CodeSpaces は GitHub が提供するクラウド上の開発環境です。[^2]
> この環境を連続で使い続けられる時間が最大で240分ということです。
> 一度タイムアウトしても、またすぐに接続することができます。

このリンク先での作業は終了です。

[^1]: [タイムアウトの設定方法])(https://docs.github.com/ja/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces#setting-your-default-timeout-period)
[^2]: [GitHub CodeSpaces について](https://github.co.jp/features/codespaces)

----

## GitHub リポジトリをフォークする

GitHub 上に Node-Red を立ち上げるためのプログラムを事前に用意しました。
以下のリンクからプロジェクトをフォーク (≒プロジェクトのコピー) をして、GitHub CodeSpaces を立ち上げましょう。

### ■[こちらの GitHub リポジトリを開いてください](https://github.com/protoout/github-codespces-node-red)  
  
`Fork` というボタンを押して `Create Fork` を行ってください。  
  
> <img width="610" alt="image" src="https://github.com/user-attachments/assets/39ed2671-fa69-42d3-bb14-e2426e123d50" />
  
> <img width="600" alt="image" src="https://github.com/user-attachments/assets/aa40f776-4a3d-439c-8f60-2e7ac49805b9" />

これであなたの GitHub 上に同じプロジェクトが複製されました。  

----

## 続いて GitHub CodeSpaces を立ち上げます

> [!IMPORTANT]
> 現在の URL が、`https://github.com/{あなたの GitHub ユーザー名}/github-codespces-node-red` になっている状態からスタートします。
  
先ほど、複製したプロジェクト上で `Code` > `Codespaces` > `Create codespaces on main` と進んでいくと、別のタブが立ち上がります。
  
> <img width="608" alt="image" src="https://github.com/user-attachments/assets/21990c36-1dbc-41a2-9405-0f1d268eda09" />  
  
画像のように、画面の右下の部分(ターミナル)でプログラムが自動で実行されますので2，3分待ちましょう。  
  
> ![image](https://github.com/user-attachments/assets/d15040aa-89b7-48e6-bf43-069d1523da5a)
>   
> 実は、フォークしたプロジェクトファイルにはこのような処理を実行するための指示が書かれています  
  
> しばらくするとターミナルの最後に `Started flow` と表示されます。これで Node-RED の準備ができました。
>   
> ![image](https://github.com/user-attachments/assets/dbf3bc02-733b-487d-9ed6-1feccb551525)
  
最後のステップです。

`ポート`タブを開くとポート1880に1つのプロセスが実行されています。  
表示範囲を`Private` > `Public` に変更し、提供されているリンクをブラウザで開いてみましょう。 

> 表示範囲は、プロセスのある位置(例えば `🔓Private` と書いてあるところ)で右クリックすると設定できます。
>   
> <img width="528" alt="image" src="https://github.com/user-attachments/assets/be44a7e4-4ad4-4112-bdb8-9978e0ed56e3" />

> 丸いインターネットのマークをクリックするか、リンクをコピーして別のタブで開けばOKです
>   
> <img width="521" alt="image" src="https://github.com/user-attachments/assets/f5e558c8-5cef-402a-b807-0a402311e80c" />
>   
> `https://XXXX-XXXX-XXXXXX-1880.app.github.dev/` のようなURLです。

  
このような Node-RED の画面が立ち上がれば準備完了です！プロジェクト機能に関する案内は `後にする` を選んで閉じてしまいましょう。

<img width="815" alt="image" src="https://github.com/user-attachments/assets/2fe24634-9477-4727-af48-88f156d44436" />

ここまで、お疲れさまでした！
  
---

**[◀ 目次ページに戻る](../readme.md)**

----

