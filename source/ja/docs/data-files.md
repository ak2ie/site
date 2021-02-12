---
title: データファイル
---

テンプレート内で、記事で直接利用できないデータを使用する必要があったり、他の場所で再利用したい場合があるでしょう。このようなユースケースのために、Hexo 3 では新しく**データファイル**を導入しました。この機能は、`source/_data` フォルダ内の YAML または JSON ファイルを読み込み、サイト内で利用できます。

{% youtube CN31plHbI-w %}

例えば、`source/_data` フォルダに `menu.yml` を追加すると、

```yaml
Home: /
Gallery: /gallery/
Archives: /archives/
```

テンプレート内でそれらを使用できます：

```
<% for (var link in site.data.menu) { %>
  <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% } %>
```

このようにレンダリングされます：

```
<a href="/"> Home </a>
<a href="/gallery/"> Gallery </a>
<a href="/archives/"> Archives </a>
```
