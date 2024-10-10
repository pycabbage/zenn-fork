---
title: "　borderとはなんぞや"
---

## borderを知ろう

CSSのborderプロパティは、要素の周りに枠線を描くために使われます。
Youtubeを例にしてみます。
![](https://storage.googleapis.com/zenn-user-upload/4b16e757ce33-20241002.png)

白いボタン要素の周りについている線がborderプロパティによって指定された線です。

### borderの使い方

borderは主に次の3つの要素で構成されています。

**太さ（border-width）**
枠線の厚さを指定します。具体的なピクセル値を使って指定できます。
例：border-width: 1px;

**スタイル（border-style）**
枠線の見た目（デザイン）を指定します。代表的な値には、solid（実線）、dashed（破線）、dotted（点線）などがあります。
例：border-style: solid;

**色（border-color）**
枠線の色を指定します。カラー名や16進数カラーコード、rgb値などが使用できます。
例：border-color: #000000;

これら3つの値を`1つのborderプロパティでまとめて指定`することが一般的です。

![](https://storage.googleapis.com/zenn-user-upload/7d67cb03b045-20241002.png)
この例では、要素に1ピクセルの黒い実線の枠線を設定しています。

また、各辺ごとに枠線を個別に指定することもできます。

border-top: 上の枠線
border-right: 右の枠線
border-bottom: 下の枠線
border-left: 左の枠線

```css:example.css
border-top: 5px dashed red;
border-right: 2px solid blue;
border-bottom: 3px dotted green;
border-left: 4px double black;
```

このようにして、要素の枠線をカスタマイズできます。

## 参考

<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model#css_%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9%E3%83%A2%E3%83%87%E3%83%AB%E3%81%A8%E3%81%AF>
