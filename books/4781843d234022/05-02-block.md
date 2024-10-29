---
title: "　インラインボックスとはなんじゃ"
---

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

