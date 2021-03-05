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

### イメージや各種ファイル追加

画像を挿入する
``` markdown
![image001](/img/image001.jpg)

```
PDFリンク
``` markdown
you can [get the PDF](/data/document.pdf) directory.
```

### タグとカテゴリ

#### タグ

ポストのタグは一つだけなら`tag`、複数なら`tags`キーを利用して、front matterで指定します。
例えば、`tag: classic hollywood` という指定であればタグは単一の"classic hollywood"として処理され、`tags: classic hollywood`の場合`["class","hollywood"]`という配列として処理されます。

全てのタグはLiquidテンプレートでは`site.tags`で参照できます。ページ上で、`site.tags`から異なる二つのアイテムが得られます。

``` html
{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}

```

#### カテゴリ

ポストのカテゴリは上記のタグと同様の働きをします。

* front matterの`category`や`categories`キーで指定します。（タグと同じロジックに従います）
* サイトに登録された全てのカテゴリは（上述のタグのforループと同様に）繰り返し処理可能な`site.categories`変数として、Liquidテンプレートに提供されます。

#### タグとカテゴリの違い

`_post`内のディレクトリはカテゴリとして扱われます。例えば、ポストのパスが

`movies/horror/_posts/2019-05-21-bride-of-chucky.markdown`なら、自動で`movies`と`horror`がそのポストのカテゴリとなります。

投稿にもカテゴリを定義するfront matterがある場合は、パスで指定されたものでなければ、既存のリストに追加されます。
カテゴリとタグの特徴的な違いは、投稿のカテゴリが投稿の生成されたURLに組み込むことが可能ですが、タグはできません。

front matterで

`category: class hollywood`と指定した場合

`movies/horror/classsic%20hollywood/2019/05/21/bride-of-chucky.html`

`categories: classic hollywood`と指定した場合

`movies/horror/classic/hollywood/2019/05/21/bride-of-chucky.html`

#### ポストの抜粋

ホストで`excerpt`変数を使用することで、抜粋にアクセスすることができます。デフォルトはポストの最初の段落ですが、
front matterや`_config.yml`で`excerpt_separator`を設定することでカスタマイズできます。


``` markdown

---
excerpt_separator: <!--more-->
---

Excerpt with multiple paragraphs

Here's another paragraph in the excerpt.
<!--more-->
Out-of-excerpt
``` 

抜粋付きのブログポストのリストを出力する例

``` html

<ul>
    {% for post in site.posts %}
    <li>
        <a href="{{ post.url }}">{{ post.title}}</a>
        {{ post.excerpt }}
    </li>
    {% endfor %}
</ul>

```

#### ドラフト

ドラフトは、ファイル名に日付を含まないポストです。作業中で、まだ公開したくないポストです。ドラフトを立ち上げるには、サイトのrootに`_drafts`フォルダを作り、最初のドラフトを作成してください。

```
.
├── _drafts
│   └── a-draft-post.md
...

```



