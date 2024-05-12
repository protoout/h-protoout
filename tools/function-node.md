# functionノードの使い方: 基本的な使い方と生成AIにコードを書かせる方法

JavaScriptをかくことができるノードです。既存のノードでできないときにこのノードを使います。

ビジュアルプログラミングツールは操作が簡単ですが、多くのそういったツールは簡単に扱える一方でできることが限られ、ある程度複雑なことをやろうとすると、「ツールの制約でできない」ということがしばしば起こります。


しかし、Node-REDはビジュアルプログラミングをベースとしながらもコードを記述できる自由度があり、既存のノードでは実現できない複雑な処理や特定の要件に対応することが可能です。


## 1. 左から来たメッセージをそのまま右に流す

functionノードは配置しただけでコードを書かなければ、何もしません。

まずは左のノードから来たメッセージを、右に流すものを作ります。

1. 3つのノードを配置し接続する
- injection
- function
- debug

<a href="https://gyazo.com/0359c41e969e04e0ec84cd79f595eb7e"><img src="https://i.gyazo.com/0359c41e969e04e0ec84cd79f595eb7e.png" alt="Image from Gyazo" width="500"/></a>


2. javascriptノードにコードをかく

```javascript

return msg;

```

この一行は、次のノードにmsgを返す、という意味です。


3. 結果

injectionノードが出力するのと同じものをfunctionノードが出力します。

<a href="https://gyazo.com/d89bdf124488ef40ae137fbc8f354597"><img src="https://i.gyazo.com/d89bdf124488ef40ae137fbc8f354597.png" alt="Image from Gyazo" width="985"/></a>

※ この例では、injectionノードが「こんにちは」を出力するように設定しています。「タイムスタンプ」の場合は数字が出力されます。


## 2. 左から来たメッセージを変更して出力する

今度はメッセージを変更する方法です。

左から来た数字を、2倍にして出力します。

1. injectノードのpayloadの設定を「数値」、「1」と設定します。

<a href="https://gyazo.com/01f91cd34458aacf19938bc8bff8921d"><img src="https://i.gyazo.com/01f91cd34458aacf19938bc8bff8921d.gif" alt="Image from Gyazo" width="500"/></a>

この状態でデプロイし、injectノードのボタンを押すと1が出力されます。

<a href="https://gyazo.com/50bc28efedf96190c931b4835365641f"><img src="https://i.gyazo.com/50bc28efedf96190c931b4835365641f.png" alt="Image from Gyazo" width="500"/></a>

2. functionノードのコードを書き換える


```javascript

msg.payload = msg.payload * 2;

return msg

```


3. 結果

デプロイしてinjectノードをクリックし、2が出力されていれば成功です。


## 3. 左から来たメッセージを変更して、複数のmsgを出力する

switchノードのように出力を複数に増やすことができます。


- 1つめ: 数字を2倍にする
- 2つめ: 左から来た数字に「月」を追加して文字列として出力する

1. functionノードの出力数を変更する

<a href="https://gyazo.com/abf23ce503c6cb1481dccf84056aed64"><img src="https://i.gyazo.com/abf23ce503c6cb1481dccf84056aed64.gif" alt="Image from Gyazo" width="922"/></a>

2. コードを書き換える

```javascript

let msg1 = { payload: msg.payload * 2 };

let msg2 = {payload: msg.payload + "月"};


return [msg1, msg2]

```

3. 結果

2つの値がそれぞれ出力されれば成功です。

<a href="https://gyazo.com/aa9531d4e56f006e461b3ae06f2b2d7f"><img src="https://i.gyazo.com/aa9531d4e56f006e461b3ae06f2b2d7f.png" alt="Image from Gyazo" width="323"/></a>


## 4. javascriptをどうやって書いたらいいか？function gtpノードを使ってコードを生成してもらおう

functionノードの使い方を簡単に説明しました。

しかし、これを使うにはjavascriptを書く必要があります。


生成AIにコーディングをお任せしちゃいましょう！


プロンプト例

```

## system
Always respond with content for a Node-RED function node, always use const or let instead of var, always return msg unless told otherwise, don't use require() unless asked to use an external node module, only respond with the code and inline code comments where necessary

## instructions

センサーの値が送られてきたら、30より大きい場合はtrue、30以下の場合false出して


```

instructions内に、作って欲しい内容を書いて生成AIにコードを作ってもらいましょう。



上記の結果

```javascript

// Check if the sensor value is greater than 30
if (msg.payload > 30) {
    msg.payload = true;
} else {
    msg.payload = false;
}

return msg;


```


---

**[◀ 目次ページに戻る](../readme.md)**