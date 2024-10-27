---
title: "　widthとはなんぞや"
---


## widthを知ろう

ボックスモデルを理解するためにまずは`width`プロパティについて説明していきます。
`width`はコンテンツの横幅を定義するためのプロパティでこれを使わなくていい場面はほぼないでしょう。至るサービスでこれは利用されています。

Youtubeのサムネイルを例にしてみてみましょう

![サムネイル500](https://storage.googleapis.com/zenn-user-upload/531a93da0716-20240913.png)

このサムネイルの画像は`width: 500px`となっており、`width`によって横幅が指定されています。
そしてこのサムネイルの横幅を半分(250px)にしてみるとサムネイルの横幅が変化することがわかると思います。
![サムネイル半分](https://storage.googleapis.com/zenn-user-upload/78f028b5ca9b-20240913.png)

このように、日々皆さんが利用しているWebサービスにおいて、画面の横幅を制御するための重要なプロパティが`width` です。

### widthを実際に使ってチャンネル登録ボタンを作ってみる

`width`のイメージは何となくつかめたでしょうか。
手を動かして自分で使ってみることで初めて理解におとしこめると思うので実際に作ってみましょう。

VSCodeを開いて`index.html`、`style.css`を作成してください。
![ファイル作成](https://storage.googleapis.com/zenn-user-upload/b063a5516970-20241001.png)
index.htmlには以下の内容を

```html:index.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>チャンネル登録ボタンを作ろう</title>
</head>

<body>
    <p>チャンネル登録</p>
</body>

</html>
```

style.cssには以下の内容を記述します。

```css:style.css
body {
    /*記事が見にくくなるので全体に背景色を入れています */
    background-color: rgb(251, 244, 236);
}
```

チャンネル登録という文字をpタグで囲うことでボックスが生成されるので、確認していきましょう。
右クリックして`検証`をクリックしてください。

![](<https://storage.googleapis.com/zenn-user-upload/b17c4a0ff893-20240914.png> =400x)

クリックすると以下のような画面が出てくると思います。
![](<https://storage.googleapis.com/zenn-user-upload/6878460dfdde-20240914.png> =600x)

ここで緑色で囲った部分をクリックしカーソルを`チャンネル登録`部分に持っていくとボックスが表示されるはずです。これでタグで囲うことで生まれる`ボックスが可視化`されました。
![](<https://storage.googleapis.com/zenn-user-upload/0b3317d45a4d-20240914.png> =600x)

`青色の部分`がコンテンツ部分です。これをwidthで操作できます。
そして、`薄いオレンジ色の部分`が指定したmarginの表示される部分です。
特に指定していないのでpadding、borderは入っていません。
:::message
`margin`を使用していないのに、margin がついているのはブラウザのデフォルトCSSによるものです。
ものによってはデフォルトでpaddingが指定されていたりと様々です。
:::

以下の記述を追加します。

```css:style.css

p {
    /* 横幅を指定 */
    width: 130px;
    /* 文字を中央に配置 */
    text-align: center;
}

```

青色のコンテンツ部分の横幅が小さくなったはずです。`右クリック`→`検証`で確認していきましょう。

![コンテンツの確認](https://storage.googleapis.com/zenn-user-upload/4112735542b1-20240915.png)

widthによって横幅を操作できることがわかったと思います。
また、`text-align: center;`によって文字を`青色部分の中央`に配置することもできました。

**次は、文字と背景に色をつけていきましょう。**

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
}
```

背景色をつけてみるとわかりやすいのですが、先ほどまで青色だったコンテンツ部分が背景色で指定した黒になっていますね。`背景色はコンテンツ部分`を黒くし、オレンジ色のmargin部分には作用しないということがここでわかるかと思います。
![](<https://storage.googleapis.com/zenn-user-upload/1b8fa36e7d8b-20240915.png> =400x)

:::message
のちほど語っていきますが、背景色はmarginには作用しませんが、paddingには作用します。気になる方は`padding: 200px;`というように追加してみてください。
paddingとmarginは余白を作りますが、余白の役割が違うことが確認できると思います。
:::
