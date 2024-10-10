---
title: "Chapter4: ボックスモデル"
---

CSSには「ボックスモデル」と呼ばれる概念があります。このボックスモデルを理解することで、`文字`と`その文字を囲っている箱`の間に自由に余白を作ることができます。

例えば、次の図では`「カテゴリ同士の間にスペースを作る」`や、`「カテゴリの箱とその中の文字の間に余裕を持たせる」`といった表現が実現できていると思います。
![](https://storage.googleapis.com/zenn-user-upload/85b0ab358b4d-20241003.png)

## ボックスモデルとは

ボックスモデルとは、テキストを生成したときに出来上がるボックスのことです。

次の図は、このボックスモデルの構造を視覚的に表しています。
![](https://storage.googleapis.com/zenn-user-upload/2d4eae25b279-20240908.png)

ボックスなんてどこにあるんだ？と思うかもしれません。でも存在しているんです。簡単に言えば、要素はすべて見えない「箱(ボックス)」のようなものに包まれているのです。
![](https://storage.googleapis.com/zenn-user-upload/91e2e1e01321-20241007.png)
この「ボックス」をカスタマイズすることで、横幅や縦幅を変更したり、余白を作ることができ、より柔軟なデザインが可能になります。

ここで言う「コンテンツ」は、`<h1>`などのタグで囲まれた文字が表示される領域を指します。
タグで囲むことでボックスを生成し、`px`を使って横幅や余白を調整できるようになります。

サイズや余白をつかさどるボックスモデルの概念を理解しなければ、Webサイトを作るのは困難を極めるでしょう。
なのでWebサイトを作成するために欠かせないボックスを操作する、5つの重要なプロパティについて学んでいきましょう。

具体的には、`width`、`height`、`padding`、`border`、`margin`の使って`Youtubeのチャンネル登録ボタン`でも作って理解を深められるようにしていきます。
![](https://storage.googleapis.com/zenn-user-upload/6599bf78f759-20240914.png)

:::message
Webサイトを作成する際、エンジニアはデザインデータに基づいて具体的なピクセル数（px）を決めていきます。例えば、ボタンのサイズやマージンなど、デザインデータで指定されたpx数を使用して実装します。
目で見て、「だいたいこれくらいのpxかぁ」とはなりません！（経験積めば多少はなりますが）

今回、チャンネル登録ボタンを作成する際も、それに近い方法でpx数を測定し皆さんに「〇〇pxと入力してください」とお願いしています。px数に関しては、僕の方で測定し指定するので`あまり気にせず進めてほしい`と考えています。
:::

最初に完成品を配布しておこうと思います。
つまずいたら利用してみてみてください。
:::details コード配布

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

```css:style.css
body {
    /* 記事が見にくくなるので全体に背景色を入れています */
    background-color: rgb(251, 244, 236);
    /* デフォルトのマージンを消す */
    /* margin: 0px; */
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
    /* デフォルトのマージンを消す */
    margin: 0px auto;
}

:::

## 参考

<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model#css_%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9%E3%83%A2%E3%83%87%E3%83%AB%E3%81%A8%E3%81%AF>

