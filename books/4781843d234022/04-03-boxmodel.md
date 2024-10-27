---
title: "　paddingとはなんぞや"
---


## paddingを知ろう

とうとうpaddingやってきましたね。
`padding`と`margin`の違いを理解できればCSSは基本的にわかるようになると思いますし、表現の幅がとても増えると思います。
まずは`paddingの基礎`を理解しましょう。
paddingはボックスモデルで表すと、緑色の部分を操るプロパティです。
![](https://storage.googleapis.com/zenn-user-upload/0ad63fe46c71-20240915.png)

paddingの特徴は以下の3つです。それぞれ解説していきます。

* 余白を作る
* 背景色が反映される
* 上下左右など指定が可能
::: message
以降実装していくのは、実験のようなものなので、みなさんは僕に習ってCSSを追加しなくて大丈夫です。
:::

### 余白を作る

`pタグ`に`padding: 100px`と指定したときに`検証`で見たボックスがこのようになります。
緑色の部分がpaddingによっってできた`余白`です。
![](<https://storage.googleapis.com/zenn-user-upload/3fcf6173917a-20240915.png> =380x)

### 背景色が反映される

paddingで作った余白には背景色が反映されます。先ほど`pタグ`に`padding: 100px`としましたが、この`pタグ`に背景色を入れていきます。
すると、先ほど作った余白部分に色がつきました。のちほど説明するmarginも同様に余白を作るプロパティです。しかしmarginはここで指定した背景色が設定されないのです。

![](<https://storage.googleapis.com/zenn-user-upload/1b2cefa57e8b-20240915.png>  =800x)

### 上下左右など指定が可能

さっきの説明では`padding: 100px`として`上下左右に余白`をつけていました。
しかし、「右だけにpadding: 100pxにしたい！」というような場合があります。「どういう時？」となるかもしれませんが、皆さんが普段目にしている綺麗なWebサイトではそういった細かい指定によって出来上がっています。綺麗であればあるほど、細かくcssで指定してあげる必要があるので、ぜひ認識だけしておいて欲しいです。

paddingの指定方法は以下の通りです。

```css:example.css
/* 上に100pxの余白*/
padding-top : 100px;
/* 右に100pxの余白 */
padding-right : 100px
/* 下に100pxの余白 */
padding-bottom : 100px;
/* 左に100pxの余白 */
padding-left : 100px;

/* 上下左右に100pxの余白 */
padding: 100px
/* 上下50px、左右100pxの余白 */
padding: 50px 100px;
 /* 上100px 左右90px 下80px */
padding: 100px 90px 80px;
/* 上100px 右90px 下80px 左70px(時計回り) */
padding: 100px 90px 80px 70px;
```

`padding: 100px 90px 80px 70px;` という指定は、四つの値が 上、右、下、左 の順番で余白が指定されるイメージです。

### paddingを実際に使ってチャンネル登録ボタンを作ってみる

やっていくのは以下の3つです。

* 文字の大きさを14pxにする（文字の大きさは最初に指定しておけばよかったですね...すみません。）
* paddingで余白を開ける
* 角丸をつける

以下のコードを追加してみてください。

```css:style.css
p{
    /* 削除 */
    /* 
    　height: 38px;
    　line-height: 38px; 
    */

    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に     */
    text-align: center;
    /* 文字の色を指定 */
    color: #fff;
    /* 背景色を指定 */
    background-color: #0f0f0f;
    /* 高さを指定 */
    font-size: 14px;
    /* 角丸にする */
    border-radius: 18px;

/* 追加 */
    /* heightの代わりにpaddingを使う */
    padding: 9px 0px;
}
```

**結果**
![](https://storage.googleapis.com/zenn-user-upload/774685199a93-20241027.png)
:::message
paddingを使って要素の高さを調整する場合と、heightプロパティを使った場合では、要素の実際の高さが少し異なることがあります。しかし、今回はpaddingの使い方に焦点を当てているため、あまり細かい違いを気にせず、**paddingを使って縦横のサイズも調整できる**という点を押さえていただければ大丈夫です。
:::

paddingの違いに焦点を当てるとこんな感じになります。

![padding9](https://storage.googleapis.com/zenn-user-upload/11a41d0bee1f-20241027.png)

paddingを利用することで`文字`と`黒のボックス`との間に余白が生まれたと思います。そして同時に`高さにも変化`が生まれることが確認できたと思います。

これで、height使わずにYoutubeのチャンネル登録ボタンの完成させることができました。
