# コレクション

コンテンツのグループ化するのに最適な方法

## セットアップ

コレクションを使用するには、まず`_config.yml`で定義します。
例として、staff membersのコレクションを作成します。

``` yaml
collections:
    - staff_members
```

## コンテンツの追加

対応するフォルダ(`_staff_members`)を作成。フォルダ以下にドキュメントを作成。
fornt matterよりあとの全部がドキュメントの`content`となる。front matterがない場合は、Jekyllは静的ファイルとしてそれ以上のコンテンツを処理しません。

front matterが存在するかどうかに関係なく、Jekyllは、コレクションのメタデータに`output:true`が設定されている場合にのみ、宛先ディレクトリに書き込みます。

上記に設定したコレクションにstaff memberを追加する方法の例です。ファイル名は`./_staff_members/jane.md`で、内容は以下とする。

``` yaml
---
name: Jane Doe
position: Developer
---
Jane has worked on Jekyll for the past *five years*.
```
内部的にコレクションとしてみなされるが、上記はpostsには適用されない。


## 出力

これで、`site.staff_members`をページで繰り返し処理して、各staff memberの内容を出力できます。ポスト同様、ドキュメント本文には`content`変数を利用してアクセスする。

``` html
{% for staff_member in site.staff_members %}
  <h2>{{ staff_member.name }} - {{ staff_member.position }}</h2>
  <p>{{ staff_member.content | markdownify }}</p>
{% endfor %}
```

コレクションの各ページをJekyllで作成したい場合は、`_config.yml`のコレクションのメタデータで、`output`キーを`true`に設定します。

``` yaml

collections:
    staff_members:
        output: true
```

`url`属性を使用して、ページにリンクを生成できます。

``` html
{% for staff_member in site.staff_members %}
  <h2>
    <a href="{{ staff_member.url }}">
      {{ staff_member.name }} - {{ staff_member.position }}
    </a>
  </h2>
  <p>{{ staff_member.content | markdownify }}</p>
{% endfor %}

```

## パーマリンク

コレクション全体のURLの出力をコントロールするのに役立つ、特別な[コレクションのパーマリンク変数](./2021/03/10/ParmaLink.html)があります。

