---
title: "　inline-blockとはなんじゃ"
---

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
