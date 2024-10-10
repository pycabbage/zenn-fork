---
title: "　CSSの基礎概念とよく使われるプロパティ"
---

このチャプターでは、CSSの基本概念を学んでいきましょう。

**学べること**

* HTMLファイルとCSSファイルの紐付け
* セレクタ、プロパティについて

## HTMLファイルとCSSファイルの紐付け

HTMLファイルとCSSファイルを紐付けるためには、HTMLの<head>タグ内で<link>タグを使います。以下のように書くと、外部CSSファイルとHTMLファイルがリンクされます。

```html:index.html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

この例では、「style.css」という名前のCSSファイルを読み込んでいます。これによって、CSSファイル内で指定したスタイルがHTMLに適用されます。

## セレクタ、プロパティ、値について

セレクタは、どのHTML要素にスタイルを適用するかを選ぶものです。
プロパティは、その要素にどんなスタイル（色や余白など）を適用するかを指定するものです。
![](<https://storage.googleapis.com/zenn-user-upload/7ba9f7c26444-20241001.png> =500x)

## 代表的なCSSプロパティ

| CSSプロパティ       | 役割                                              |
|--------------------|--------------------------------------------------|
| color              | テキストの色                                       |
| font-size          | テキストのサイズ                                   |
| background-color   | 要素の背景色                                       |
| text-align         | テキストの配置（左寄せ、中央寄せ、右寄せ）         |
| width              | 要素の幅                                           |
| height             | 要素の高さ                                         |
| padding            | 要素の内側の余白                                   |
| margin             | 要素の外側の余白                                   |
| border             | 要素の枠線を定義                                   |
| display            | 要素の表示形式を定義（ブロック、インライン、フレックスなど） |

その中でも`width`、`height`、`padding`、`margin`、`border`までは丁寧に説明しないと理解を誤る恐れがあるので、ボックスモデルのchapterで紹介していきます。

ひとまずこのチャプターでは`color`、`font-size`、`background-color`、`text-align`、`border-radius` を軽く説明します。

### color : 文字の色を変える

```css:example.css
color: blue
```

**結果**
![](https://storage.googleapis.com/zenn-user-upload/cf1b6f36f7a6-20241001.png)

### font-size : 文字の大きさを指定する

```css:example.css
font-size: 50px;
```

**結果**
![](https://storage.googleapis.com/zenn-user-upload/f0682b13bdfd-20241001.png)

### background-color : 背景色を指定する

```css:example.css
    background-color: #fbf4ec;
```

**結果**
![](<https://storage.googleapis.com/zenn-user-upload/5fdd5792c6a0-20241001.png> =400x)

### text-align : 文字の位置を指定する

```css:example.css
   text-align:center
```

**結果**
![](https://storage.googleapis.com/zenn-user-upload/4700b1a0c3c9-20241001.png)

## 参考

<https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Selectors>
