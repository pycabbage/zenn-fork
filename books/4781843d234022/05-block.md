---
title: "Chapter5: ブロックボックスとインラインボックス"
---
このチャプターでは手を動かさなくても問題ありませんが、実際に試してみたい方はぜひチャレンジしてみてください。

## ブロックボックスとインラインボックスとは

<!-- TODO: chatgptの要約文を使って2000文字に抑える。必要なものを省かないように自分で添削 -->

チャプター4ではボックスのボックスモデルについて学びましたが、ボックスにも種類があります。
主にボックスは**ブロックボックス**、**インラインボックス**で構成されており、これらの違いがわからないと**widthを指定したのに期待通りに動作しない**などの事態が発生します。
そういったトラブルに対処していただくためにも、2つの違いについて解説していきたいと思います。

![ブロックボックスとインラインボックス](https://storage.googleapis.com/zenn-user-upload/a0cbda4282ea-20241024.png)

まず、**ブロックボックスは横幅いっぱいに広がり、次の要素がその下に表示されます**。例えば、`<div>`や`<h1>`などはブロックボックスに分類されます。これらは自動的に改行し、他の要素と重ならないようになっています。

一方、**インラインボックスは必要な幅だけ使用し、次の要素と同じ行に並んで表示されます**。`<span>`や`<a>`、`<strong>`などがこれに該当します。

## ブロックボックスとインラインボックスの基礎

ボックスには、ブロックボックスとインラインボックスの2種類があり、それぞれの表示形式(ブロックボックス、インラインボックス)はタグごとにデフォルトで設定されています。
そして、表示型の指定は、**displayプロパティ**を使って行うことができます。

| display | HTMLタグ |
| ---- | ---- |
| block | `<h1>` , `<p>` , `<div>`|
| inline | `<a>` , `<span>` , `<img>` |

:::message
<h1> や <p>、<div> のように、`display: block` を持つ要素を**ブロック要素**と呼びます。
一方で、<a>、<span>、<img> のように、`display: inline` を持つ要素は**インライン要素**と呼ばれます。
:::

デフォルトでついてるボックスの表示型を変更したい場合は`displayプロパティ`を利用します。

`display:block`とすると、その要素はブロックボックスとなり

```css:example.css
display:block
```

`display:inline`とすると、その要素はインラインボックスとなります。

```css:example.css
display:inline
```

それでは二つの違いについてさらに詳細に説明していきましょう。

## ブロックボックスとは

ブロックボックスの特徴は以下の通りです

* 要素が改行される
* width、heightが適用される
* padding、marginが適用される
* 親要素いっぱいの幅をとる

「これって当たり前の動きじゃないの？」って思う方もいるかもしれません。
**デフォルトでdisplay:blockの表示型をとっているタグが多い**ので、これが要素の当たり前の挙動だと捉えてしまうのも無理はありません。
代表的なのは`<h1>` , `<p>` , `<div>`とよく使用されるタグですね。
ブロックボックスは、widthやheightなどのプロパティを使用すると、意図通りに動作します。一方で、このノリで**インラインボックスにwidth、height、padding、marginを指定すると反映されない**ということがあります。

## インラインボックスとは

インラインボックスの特徴は以下の通りです。

* 要素が改行されない
* width、heightが適用されない
* padding、marginは適用されるが、他のインラインボックスをこのボックスから引き離すことはない
* 要素の内容に応じた幅をとる(テキストや画像の大きさに応じて、ボックスの幅が自動的に決定)

これらの特徴を完全に理解する必要はありません。
理解して欲しいのは、インラインボックスが適用された要素だと**改行されない**のと**width、height、padding、marginプロパティが期待通りに動作しない**と言うことです。

どう言う時にインラインボックスであることが困るのでしょうか？例を挙げてみます。

### 例 : ボタンを作る時

こんな感じのボタンを作りたかったとしましょう。
![ボタン](https://storage.googleapis.com/zenn-user-upload/3499c52b9411-20241024.png)

何か別ページに移動するボタンを作りたいと思った時に、aタグを使うのが一般的なので使用します。

```html:example.html
<a href="#">ボタン</a>
```

そして、このaタグは**デフォルトでインラインボックス**になっているので、widthを利用して横幅を調整しようと思っても期待通りに動作しません。

```css:example.css
/* aタグはインライン要素だから、widthが適用されない */
/* paddingは一応適用される */
a {
    width: 200px;
    text-align: center;
    padding: 5px 25px;
    border-radius: 150px;
    background-color: rgb(175, 216, 227);
}
```

**結果**
![インラインボタン](https://storage.googleapis.com/zenn-user-upload/d35e432a2d58-20241024.png)

widthが適用されていませんね。
そんな時にdisplayプロパティでblockに変えてあげることで横幅を調整できるようになります。

```css:example.css
a {
    width: 200px;
    text-align: center;
    padding: 5px 25px;
    border-radius: 150px;
    background-color: rgb(175, 216, 227);
    /* widthが適用される */
    display: block;
}
```

![ブロック適用](https://storage.googleapis.com/zenn-user-upload/5e5602224dfd-20241024.png)

どうでしょうか。ブロックボックスとインラインボックスの違いについて理解できたでしょうか。

## inline-blockとは

`display: inline-block`は、**横に並べたいけど大きさも調整したい**ときに使う特別な設定です。通常、**inlineだと横に並ぶけど大きさが設定できないし、blockだと大きさは自由だけど改行されて**しまいます。
inline-blockを使うと、この2つの良いところを組み合わせた動きができます。

* 横に並ぶ（改行しない）
* 大きさが自由（widthやheightを設定できる）

:::message
ブロック要素は改行されてしまいます。
![ブロック要素](https://storage.googleapis.com/zenn-user-upload/63f8d1b90afd-20241025.png)
:::

display:blockの記述をinline-blockに変えてみます。

```css:style.css
a {
    width: 200px;
    text-align: center;
    padding: 5px 25px;
    border-radius: 150px;
    background-color: rgb(175, 216, 227);
    /* 改行されない&width,heightがok */
    display: inline-block;
}
```

そうするとボタンが二つ並ぶようになります。
![インラインボックス](https://storage.googleapis.com/zenn-user-upload/5363dcc1f116-20241025.png)

参考 : <https://qiita.com/tosagatuo/items/c8b51150d20527df216d>

## 参考

**ブロックボックスとインラインボックス**
<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model#%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9%E3%81%A8%E3%82%A4%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9>
<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model#%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9%E3%81%A8%E3%82%A4%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9>

**inline-block**
<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model#display_inline-block_%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B>
