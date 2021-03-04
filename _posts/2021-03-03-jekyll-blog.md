---
layout: post
title: jekyll Blog Function
category: jekyll

---

# jekyllのブログ機能

## _posts　フォルダ

_postsフォルダを作成し、指定されたファイル名.mdで保存するとhtml形式のファイルが自動生成されます。

```
yyyy-mm-dd-blog_title.md
```

【記述例】

```
2021-03-03-hinamatsuri.md
2021-02-03-setsubun.md
```

## Front Matter

MarkDown形式のファイルの先頭に、YAML形式のfront matterブロックを追加することでJekyllは
特別なファイルとして、処理します。以下に記述例です。

``` markdown
---
 layout: post
 title: "blog"
---
```

### 定義済みのグローバル変数

|変数|説明|　|
|:--|:--|:-:|
|layout|設定したらそのレイアウトファイルを使用する。レイアウトファイルの愛芽を拡張子なしで記述する。レイアウトファイルは_layoutsディレクトリに格納する。nullを使用するとレイアウトファイルを使用しない。||
| permalink | サイト全体のURLのスタイル（デフォルトは/year/month/day/title.html） | |
| published | サイト生成するときに、特定のポストを表示したくない場合はfalse| ||
||||
|date| ポストのファイル名からの日付を上書き。特殊フォーマットで、時刻とタイムゾーンはオプション。 |YYYY-MM-DD HH:MM:SS +/-TTTT|
|category <br/>categories|ポストをフォルダ分けする代わりに、１つ以上のカテゴリを設定できる。サイトにポストを生成する時に、これらのカテゴリが設定されているように振る舞います。||
|tags|カテゴリによく似ており、1つ以上のタグをポストに追加できます||

### イメージやリソースを含める

画像を挿入する
``` markdown
![image001](/img/image001.jpg)

```
PDFリンク
``` markdown
you can [get the PDF](/data/document.pdf) directory.
```

