---
title: "　marginとはなんぞや"
---

## marginを知ろう

marginはとても大切です。Webサイトのあらゆるところで使用されている余白を作るプロパティだからです。

特にその効果が発揮されるのが、Webサイトを作る時です。しかし、今回のような`チャンネル登録ボタン`を作るという企画では十分な恩恵は感じられないと思いますが、最低限の動作を学んでいきたいと思います。

**よく使われるmarginの使い方3つを紹介していきます。**

* 要素と要素の間に間を作る
* 複数の要素を中央に配置する
* 上下左右など指定

### 要素と要素の間に間を作る

Youtubeのカテゴリを例に取ってみてみましょう。

![](https://storage.googleapis.com/zenn-user-upload/22caed728a17-20240927.png)

オレンジ色のところがmarginで、`カテゴリとカテゴリの間の余白`として利用されているのがわかるかともいます。

これを見るとpaddingは`黒のボックスの中`で利用されおり`文字とボックスに余白`を開けるために利用されています。一方でmarginは`ボックスの外側`で`ボックス同士を引き離すため`に利用されているのがわかると思います。

![](https://storage.googleapis.com/zenn-user-upload/c7293a54fda5-20240929.png)

marginは要素（タグで囲ったもの）と要素に余白を与え引き離す役割があるのです。だから背景色を適用しても色がつかないのですね。

### 複数の要素を中央に配置する

さらにmarignには要素を中央に配置するといった役割もあります。
このブログ記事を掲載してくれている`zenn`で具体例を見てみましょう。

ここでは記事の塊が中央に並んでいるのがわかると思います。
![](https://storage.googleapis.com/zenn-user-upload/5048fdc0ccd2-20240929.png)
検証でこれをみていくとmarginによって中央に配置されているのがわかると思います。marginによってさまざまなものをまとめて中央に配置できるのです。
![](https://storage.googleapis.com/zenn-user-upload/2d0cec884b90-20240927.png)

### 上下左右など指定が可能

marginはpaddingと同様の指定方法です。

```css:example.css
 /* 上に100pxの余白*/
margin-top : 100px;
/* 右に100pxの余白 */
margin-right : 100px
/* 下に100pxの余白 */
margin-bottom : 100px;
/* 左に100pxの余白 */
margin-left : 100px;

/* 上下左右に100pxの余白 */
margin: 100px
/* 上下50px、左右100pxの余白 */
margin: 50px 100px;
 /* 上100px 左右90px 下80px */
margin: 100px 90px 80px;
/* 上100px 右90px 下80px 左70px(時計回り) */
margin: 100px 90px 80px 70px;
```

### marginを使ってみよう

現状デフォルトCSSによって、指定していないmarginが効いている状態です。

![](<https://storage.googleapis.com/zenn-user-upload/5a6aba998ff1-20240925.png> =400x)

それを消していきます。body、pタグに`margin:0px`を指定します。
:::message
pタグだけでなくbodyにもデフォルトmarginが付与されています。
:::

```css:style.css
body {
    /* 記事が見にくくなるので全体に背景色を入れています */
    background-color: rgb(251, 244, 236);

/* 追加 */
    /* デフォルトのマージンを消す */
    margin: 0px;
}

p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 文字を中央に配置 */
    text-align: center;


    /* 文字の大きさを指定 */
    font-size: 14px;
    /* 上下に8px、左右に5pxの余白 */
    padding: 8px 5px;
    /* 角丸を指定 */
    border-radius: 18px;

/* 追加 */    
    /* デフォルトのマージンを消す */
    margin: 0px;
}
```

結果、デフォルトmarginが消えて左上にピッタシボタンがくっついたと思います。
![](https://storage.googleapis.com/zenn-user-upload/1cd3c8f3ca05-20240925.png)

:::message
ちなみに0pxの場合は、pxを省略しても問題ありません。

```css:example.css
  margin: 0;
```

:::

次はチャンネル登録ボタン全体を中央に配置したいと思います。
先ほど書いた`margin: 0px`を削除し`margin: 0px auto;`を追加してください

```css:style.css
body {
    /* 記事が見にくくなるので全体に背景色を入れています */
    background-color: rgb(251, 244, 236);
    /* デフォルトのマージンを消す */
    margin: 0px;
}

p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 文字を中央に配置 */
    text-align: center;


    /* 文字の大きさを指定 */
    font-size: 14px;
    /* 上下に8px、左右に5pxの余白 */
    padding: 8px 5px;
    /* 角丸を指定 */
    border-radius: 18px;

/* 追加 */    
    /* デフォルトのマージンを消す */
    margin: 0px auto;
}
```

![](https://storage.googleapis.com/zenn-user-upload/b71da779945e-20241001.png)

:::message
真ん中にするならtext-align:centerで良くないか？と思った方もいるかもしれません。
あくまでも、text-align:centerはボックスの内部にあるテキストを中央に配置するものであって、ボックス(要素)そのものを中央に配置するわけではありません。

* テキストを真ん中にしたいなら`text-align: center`
* ボックスを中央にしたいなら`margin: 0 auto`

autoを左右に指定すると要素が中央に配置されます。

:::
