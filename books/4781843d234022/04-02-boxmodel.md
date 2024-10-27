---
title: "　heightとはなんぞや"
---


## heightを知ろう

`height`プロパティについて見ていきましょう。heightは青色の高さを指定するプロパティです。

![](https://storage.googleapis.com/zenn-user-upload/310050b983b8-20240915.png)
「めちゃめちゃ使えそうだなぁ」と考える方も多いと思いますが、頻繁に使うプロパティではないという印象が個人的にあります。
なぜなら、基本的に`paddingプロパティ`で高さを操るからです。`チャンネル登録ボタン`を作るこの記事でも`padding`で高さを調節していきますので、heightは軽く説明していきます。

:::message
**なぜheightが使われないのか？**
height は、要素全体の高さをピクセルで固定してしまうため、コンテンツが増減するとレイアウト(デザイン)が崩れることがあります。例えば、テキストの量が多いとき、高さが足りなくなることがあります。
:::

### heightを実際に使ってみる

皆さんは手を動かさなくて大丈夫です。
先ほどのCSSにheightを追加していきましょう。より変化がわかりやすいように極端な数字を使います。

```css:style.css
p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に配置 */
    text-align: center;
     /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 文字の大きさ */
    font-size: 14px;

/* 追加 */    
    /* コンテンツの高さを指定 */
    height: 400px;   
}
```

結果
![](<https://storage.googleapis.com/zenn-user-upload/745942ebe26b-20240915.png> =300x)
高さが変化したことはおわかりいただけたでしょうか。
しっかりと背景色がついていることも確認できたかと思います。
そうです。これがheightです。シンプル！

このheightはどんなことをするのか体験してもらいたくて使っただけなので元に戻します。

```css:style.css
p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に配置 */
    text-align: center;
     /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
}

```

### heightを実際に使ってチャンネル登録ボタンを作ってみる

ボタンに高さを指定したいので以下の記述を追加してみてください。

```css:style.css
p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に配置 */
    text-align: center;
     /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 文字の大きさ */
    font-size: 14px;

/* 追加 */
    /* 高さを指定 */
    height: 38px;
    /* 垂直の中央配置 */
    line-height: 38px;
}

```

**結果**
![四角ボタン完成](https://storage.googleapis.com/zenn-user-upload/d7799ace1f4b-20241027.png)

そして、チャンネル登録ボタン風にするために、角を丸くしていきます

```css:style.css
p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に配置 */
    text-align: center;
    /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 高さを指定 */
    font-size: 14px;
    /* 垂直の中央配置 */
    line-height: 38px;


/* 追加 */
    /* 角丸にする */
    border-radius:18px
}
```

**結果**
![ボタンひとまず完成](https://storage.googleapis.com/zenn-user-upload/095a2685de9f-20241027.png)

ひとまず完成ということになりますが、heightではなくpaddingを使ったやり方を次に説明していきます。
