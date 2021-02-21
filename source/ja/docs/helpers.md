---
title: ヘルパー
---

ヘルパーを使うと、テンプレートでスニペットをすぐに挿入できます。ヘルパーはソースファイルでは使用できません。

簡単に[独自のカスタムヘルパーを作る](https://hexo.io/api/helper.html) か、作成済のヘルパーも使用できます。

{% youtube Uc53pW0GJHU %}

## URL

### url_for

先頭にルートパスを付けた URL を返します。自動的にエンコードされて出力されます。

```js
<%- url_for(path, [option]) %>
```

| オプション | 説明             | デフォルト値               |
| ---------- | ---------------- | -------------------------- |
| `relative` | 相対パスでの出力 | `config.relative_link`の値 |

**例：**

```yml
_config.yml
root: /blog/ # 例
```

```js
<%- url_for('/a/path') %>
// /blog/a/path
```

相対リンクにするかは、デフォルトで`relative_link`オプションの値を参照します。
例： 記事とページのパスは '/foo/bar/index.html' になります。

```yml
_config.yml
relative_link: true
```

```js
<%- url_for('/css/style.css') %>
// ../../css/style.css

/* オプションの上書き
 * `relative_link`を有効にした場合でも、
 * それを無効化して絶対パスのリンクを出力することもできますし、その逆も可能です。
 */
<%- url_for('/css/style.css', {relative: false}) %>
// /css/style.css
```

### relative_url

`from` から見た `to` の相対パスを返します。

```js
<%- relative_url(from, to) %>
```

**例：**

```js
<%- relative_url('foo/bar/', 'css/style.css') %>
// ../../css/style.css
```

### full_url_for

`config.url` を先頭に付けた URL を返します。自動的にエンコードされて出力されます。

```js
<%- full_url_for(path) %>
```

**例：**

```yml
_config.yml
url: https://example.com/blog # 例
```

```js
<%- full_url_for('/a/path') %>
// https://example.com/blog/a/path
```

### gravatar

メールアドレスから gravatar の画像 URL を返します。

[options]パラメータが未設定の場合、デフォルトオプションが適用されます。その他に、Gravatar に渡すサイズパラメータの数値を設定できます。最後に、オブジェクトを設定すると、Gravatar へのクエリ文字列に変換されます。

```js
<%- gravatar(email, [options]) %>
```

| オプション | 説明                 | デフォルト値 |
| ---------- | -------------------- | ------------ |
| `s`        | 出力画像サイズ       | 80           |
| `d`        | デフォルト画像       |
| `f`        | デフォルト画像の強制 |
| `r`        | レーティング         |

追加情報： [Gravatar](https://ja.gravatar.com/site/implement/images/)

**例：**

```js
<%- gravatar('a@abc.com') %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787

<%- gravatar('a@abc.com', 40) %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787?s=40

<%- gravatar('a@abc.com' {s: 40, d: 'https://via.placeholder.com/150'}) %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787?s=40&d=https%3A%2F%2Fvia.placeholder.com%2F150
```

## HTML タグ

### css

CSS ファイルを読み込みます。 `path` には文字列または配列を指定できます。 `path` は文字列や配列、オブジェクト、オブジェクトの配列も指定可能です。`path`に`.css`拡張子が含まれる場合、自動的に[`/<root>/`](/ja/docs/configuration#URL)の値が先頭に付与されます。任意の属性にはオブジェクトを使用します。

```js
<%- css(path, ...) %>
```

**Examples:**

```js
<%- css('style.css') %>
// <link rel="stylesheet" href="/style.css">

<%- css(['style.css', 'screen.css']) %>
// <link rel="stylesheet" href="/style.css">
// <link rel="stylesheet" href="/screen.css">

<%- css({ href: 'style.css', integrity: 'foo' }) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">

<%- css([{ href: 'style.css', integrity: 'foo' }, { href: 'screen.css', integrity: 'bar' }]) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">
// <link rel="stylesheet" href="/screen.css" integrity="bar">
```

### js

JavaScript ファイルを読み込みます。`path`には文字列や配列、オブジェクト、オブジェクトの配列を使用できます。`path`に`.js`拡張子が含まれる場合、自動的に[`/<root>/`](/ja/docs/configuration#URL)の値が先頭に付与されます。任意の属性にはオブジェクトを使用します。

```js
<%- js(path, ...) %>
```

**例：**

```js
<%- js('script.js') %>
// <script src="/script.js"></script>

<%- js(['script.js', 'gallery.js']) %>
// <script src="/script.js"></script>
// <script src="/gallery.js"></script>

<%- js({ src: 'script.js', integrity: 'foo', async: true }) %>
// <script src="/script.js" integrity="foo" async></script>

<%- js([{ src: 'script.js', integrity: 'foo' }, { src: 'gallery.js', integrity: 'bar' }]) %>
// <script src="/script.js" integrity="foo"></script>
// <script src="/gallery.js" integrity="bar"></script>
```

### link_to

リンクを挿入します。

```js
<%- link_to(path, [text], [options]) %>
```

| オプション | 説明                     | デフォルト値 |
| ---------- | ------------------------ | ------------ |
| `external` | 新しいタブでリンクを開く | false        |
| `class`    | クラス名                 |
| `id`       | ID                       |

**Examples:**

```js
<%- link_to('http://www.google.com') %>
// <a href="http://www.google.com" title="http://www.google.com">http://www.google.com</a>

<%- link_to('http://www.google.com', 'Google') %>
// <a href="http://www.google.com" title="Google">Google</a>

<%- link_to('http://www.google.com', 'Google', {external: true}) %>
// <a href="http://www.google.com" title="Google" target="_blank" rel="noopener">Google</a>
```

### mail_to

メールリンクを挿入します。

```js
<%- mail_to(path, [text], [options]) %>
```

| オプション | 説明       |
| ---------- | ---------- |
| `class`    | クラス名   |
| `id`       | ID         |
| `subject`  | メール件名 |
| `cc`       | CC         |
| `bcc`      | BCC        |
| `body`     | メール本文 |

**例：**

```js
<%- mail_to('a@abc.com') %>
// <a href="mailto:a@abc.com" title="a@abc.com">a@abc.com</a>

<%- mail_to('a@abc.com', 'Email') %>
// <a href="mailto:a@abc.com" title="Email">Email</a>
```

### image_tag

画像を挿入します。

```js
<%- image_tag(path, [options]) %>
```

| オプション | 説明               |
| ---------- | ------------------ |
| `alt`      | 画像の代替テキスト |
| `class`    | クラス名           |
| `id`       | ID                 |
| `width`    | 画像の幅           |
| `height`   | 画像の高さ         |

### favicon_tag

favicon を挿入します。

```js
<%- favicon_tag(path) %>
```

### feed_tag

フィードのリンクを挿入します。

```js
<%- feed_tag(path, [options]) %>
```

| オプション | 説明               | デフォルト値   |
| ---------- | ------------------ | -------------- |
| `title`    | フィードのタイトル | `config.title` |
| `type`     | フィードの種類     | atom           |

**例：**

```js
<%- feed_tag('atom.xml') %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">

<%- feed_tag('rss.xml', { title: 'RSS Feed', type: 'rss' }) %>
// <link rel="alternate" href="/atom.xml" title="RSS Feed" type="application/atom+xml">

/* Defaults to hexo-generator-feed's config if no argument */
<%- feed_tag() %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">
```

## 条件タグ

### is_current

`path` が現在のページの URL と一致するかチェックします。厳密なマッチングには`strict`を使用します。

```js
<%- is_current(path, [strict]) %>
```

### is_home

現在のページがホームページであるかチェックします。

```js
<%- is_home() %>
```

### is_post

現在のページが記事であるかチェックします。

```js
<%- is_post() %>
```

### is_page

現在のページがページであるかチェックします。

```js
<%- is_page() %>
```

### is_archive

現在のページがアーカイブページであるかチェックします。

```js
<%- is_archive() %>
```

### is_year

現在のページが年ごとのアーカイブページであるかチェックします。

```js
<%- is_year() %>
```

### is_month

現在のページが月ごとのアーカイブページであるかチェックします。

```js
<%- is_month() %>
```

### is_category

現在のページがカテゴリーページであるかチェックします。
引数に文字列を指定すると、現在のページが指定されたタグと一致するかチェックします。

```js
<%- is_category() %>
<%- is_category('hobby') %>
```

### is_tag

現在のページがタグページであるかチェックします。
引数に文字列を指定すると、現在のページが指定されたタグと一致するかチェックします。

```js
<%- is_tag() %>
<%- is_tag('hobby') %>
```

## 文字列操作

### trim

文字列の先頭と末尾の空白を除去します。

```js
<%- trim(string) %>
```

### strip_html

文字列内の全ての HTML タグを除去します。

```js
<%- strip_html(string) %>
```

**例：**

```js
<%- strip_html('It\'s not <b>important</b> anymore!') %>
// It's not important anymore!
```

### titlecase

文字列を適切に英語タイトルの大文字化します。

```js
<%- titlecase(string) %>
```

**例：**

```js
<%- titlecase('this is an apple') %>
# This is an Apple
```

### markdown

MarkDown の文字列をレンダリングします。

```js
<%- markdown(str) %>
```

**例：**

```js
<%- markdown('make me **strong**') %>
// make me <strong>strong</strong>
```

### render

文字列をレンダリングします。

```js
<%- render(str, engine, [options]) %>
```

**例：**

```js
<%- render('p(class="example") Test', 'pug'); %>
// <p class="example">Test</p>
```

詳しくは[Rendering](https://hexo.io/ja/api/rendering)を参照してください。

### word_wrap

テキストを `length` 以下の長さの行に折り返します。デフォルトでは `length` は 80 です。

```js
<%- word_wrap(str, [length]) %>
```

**例：**

```js
<%- word_wrap('Once upon a time', 8) %>
// Once upon\n a time
```

### truncate

指定した長さ `length` にテキストを切り詰めます。デフォルトでは 30 文字です。

```js
<%- truncate(text, [options]) %>
```

**例：**

```js
<%- truncate('昔々あるところに、お爺さんとお婆さんが', {length: 17}) %>
// 昔々あるところに、お爺さんと...

<%- truncate('Once upon a time in a world far far away', {length: 17, separator: ' '}) %>
// Once upon a...

<%- truncate('そして、多くの人がよく眠れていることが分かりました。', {length: 25, omission: '... (続き)'}) %>
// そして、多くの人がよく眠れているこ... (続き)
```

### escape_html

文字列内の HTML 要素をエスケープします。

```js
<%- escape_html(str) %>
```

**例：**

```js
<%- escape_html('<p>Hello "world".</p>') %>
// &lt;p&gt;Hello &quot;world&quot;.&lt;&#x2F;p&gt;
```

## テンプレート

### partial

他のテンプレートファイルを読み込みます。`locals`でローカル変数を定義できます。

```js
<%- partial(layout, [locals], [options]) %>
```

| オプション | 説明                                                                   | デフォルト値 |
| ---------- | ---------------------------------------------------------------------- | ------------ |
| `cache`    | コンテンツをキャッシュ（フラグメントキャッシュを使用）                 | `false`      |
| `only`     | 厳密なローカル変数。テンプレートの`locals`で設定された変数のみを使用。 | `false`      |

### フラグメントキャッシュ

コンテンツの断片をキャッシュします。断片内のコンテンツを保存し、次のリクエストが来たらキャッシュを配信します。

```js
<%- fragment_cache(id, fn);
```

**例：**

```js
<%- fragment_cache('header', function(){
  return '<header></header>';
}) %>
```

## 日付と時刻

### date

フォーマットを指定して日付を挿入します。`date`は UNIX 時間や ISO 表記、date オブジェクト、[Moment.js]のオブジェクトを使用できます。`format`にはデフォルトで `date_format`が設定されます。

```js
<%- date(date, [format]) %>
```

**例：**

```js
<%- date(Date.now()) %>
// 2013-01-01

<%- date(Date.now(), 'YYYY/M/D') %>
// Jan 1 2013
```

### date_xml

XML フォーマットの日付を挿入します。`date`は UNIX 時間や ISO 表記、date オブジェクト、[Moment.js]のオブジェクトを使用できます。

```js
<%- date_xml(date) %>
```

**例：**

```js
<%- date_xml(Date.now()) %>
// 2013-01-01T00:00:00.000Z
```

### time

フォーマットを指定して時刻を挿入します。`date`は UNIX 時間や ISO 表記、date オブジェクト、[Moment.js]のオブジェクトを使用できます。`format`にはデフォルトで `time_format`が設定されます。

```js
<%- time(date, [format]) %>
```

**例：**

```js
<%- time(Date.now()) %>
// 13:05:12

<%- time(Date.now(), 'h:mm:ss a') %>
// 1:05:12 pm
```

### full_date

フォーマットを指定して日付と時刻を挿入します。`date`は UNIX 時間や ISO 表記、date オブジェクト、[Moment.js]のオブジェクトを使用できます。`format`にはデフォルトで `date_format + time_format`が設定されます。

```js
<%- full_date(date, [format]) %>
```

**例：**

```js
<%- full_date(new Date()) %>
// Jan 1, 2013 0:00:00

<%- full_date(new Date(), 'dddd, MMMM Do YYYY, h:mm:ss a') %>
// Tuesday, January 1st 2013, 12:00:00 am
```

### moment

[Moment.js] ライブラリです。

## リスト

### list_categories

全カテゴリのリストを挿入します。

```js
<%- list_categories([options]) %>
```

| オプション   | 説明                                                                                                                                                       | デフォルト値 |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `orderby`    | カテゴリの並び順                                                                                                                                           | name         |
| `order`      | 並べ方。 昇順なら`1`または`asc`。降順なら`-1`または`desc`。                                                                                                | 1            |
| `show_count` | カテゴリごとに記事数を表示                                                                                                                                 | true         |
| `style`      | カテゴリリストを表示する際のスタイル。 `list`を指定すると並び替えずに表示。                                                                                | list         |
| `separator`  | カテゴリ間の区切り。 (`style`に`list`が指定されない場合のみ適用)                                                                                           | ,            |
| `depth`      | 表示するカテゴリの最大階層。 `0`を指定すると、全カテゴリと子カテゴリを表示。`-1`は `0`に似ていますが、同一階層に表示。 `1`は最上位階層のカテゴリのみ表示。 | 0            |
| `class`      | カテゴリリストのクラス名                                                                                                                                   | category     |
| `transform`  | カテゴリ名の表示を変更するための関数                                                                                                                       |
| `suffix`     | リンクにに追加する接尾辞                                                                                                                                   | なし         |

**例：**

```js
<%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return titlecase(str);
  }
}) %>

<%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return str.toUpperCase();
  }
}) %>
```

### list_tags

全タグのリストを挿入します。

```js
<%- list_tags([options]) %>
```

| オプション   | 説明                                                                                       | デフォルト値 |
| ------------ | ------------------------------------------------------------------------------------------ | ------------ |
| `orderby`    | カテゴリの並び順                                                                           | name         |
| `order`      | 並べ方。 昇順なら`1`または`asc`。降順なら`-1`または`desc`。                                |
| `show_count` | タグごとに記事数を表示                                                                     | true         |
| `style`      | タグリストを表示する際のスタイル。 `list`を指定すると並び替えずに表示。                    | list         |
| `separator`  | タグ間の区切り。 (`style`が`list`でない場合のみ適用)                                       | ,            |
| `class`      | タグリストのクラス名（文字列）または、タグのクラスごとのカスタム（オブジェクト、下記参照） | tag          |
| `transform`  | タグ名の表示を変更するための関数。[list_categories](#list-categories)の例を参照。          |
| `amount`     | 表示するタグ数。(0 = 無制限）                                                              | 0            |
| `suffix`     | リンクに追加する接尾辞                                                                     | None         |

クラスの上級拡張：

| オプション    | 説明                                                                                                        | デフォルト値                                                 |
| ------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `class.ul`    | `<ul>`のクラス名 (`list`スタイルのみで使用可能)                                                             | `tag-list` (リストスタイル)                                  |
| `class.li`    | `<li>` のクラス名 (`list`スタイルのみで使用可能)                                                            | `tag-list-item` (リストスタイル)                             |
| `class.a`     | `<a>` のクラス名                                                                                            | `tag-list-link` (リストスタイル) `tag-link` (通常スタイル)   |
| `class.label` | タグの階層が含まれる`<span>`のクラス名 (`class.label`を設定したとき`<span>`に通常スタイルでのみ使用可能。 ) | `tag-label` (normal style)                                   |
| `class.count` | タグ数が含まれる`<span>` のクラス名 (`show_count` が `true`の場合のみ使用可能)                              | `tag-list-count` (リストスタイル) `tag-count` (通常スタイル) |

例：

```ejs
<%- list_tags(site.tags, {class: 'classtest', style: false, separator: ' | '}) %>
<%- list_tags(site.tags, {class: 'classtest', style: 'list'}) %>
<%- list_tags(site.tags, {class: {ul: 'ululul', li: 'lilili', a: 'aaa', count: 'ccc'}, style: false, separator: ' | '}) %>
<%- list_tags(site.tags, {class: {ul: 'ululul', li: 'lilili', a: 'aaa', count: 'ccc'}, style: 'list'}) %>
```

### list_archives

アーカイブリストを挿入します。

```js
<%- list_archives([options]) %>
```

| Option       | Description                                                                              | Default   |
| ------------ | ---------------------------------------------------------------------------------------- | --------- |
| `type`       | 種類。`yearly`または`monthly`を設定可能。                                                | monthly   |
| `order`      | 並べ方。 昇順なら`1`または`asc`。降順なら`-1`または`desc`。                              | 1         |
| `show_count` | アーカイブごとに記事数を表示                                                             | true      |
| `format`     | 日付フォーマット                                                                         | MMMM YYYY |
| `style`      | アーカイブリストを表示する際のスタイル。`list`を指定すると並び替えずにアーカイブを表示。 | list      |
| `separator`  | アーカイブ間の区切り。 (`style`が`list`でない場合のみ適用)                               | ,         |
| `class`      | アーカイブリストのクラス名                                                               | archive   |
| `transform`  | アーカイブ名の表示を変更するための関数。[list_categories](#list-categories)の例を参照    |

### list_posts

記事のリストを挿入します。

```js
<%- list_posts([options]) %>
```

| Option      | Description                                                                        | Default |
| ----------- | ---------------------------------------------------------------------------------- | ------- |
| `orderby`   | 記事の並び順                                                                       | date    |
| `order`     | 並べ方。 昇順なら`1`または`asc`。降順なら`-1`または`desc`。                        | 1       |
| `style`     | 記事リストを表示する際のスタイル。`list`を指定すると並び替えずにアーカイブを表示。 | list    |
| `separator` | 記事間の区切り。 (`style`が`list`でない場合のみ適用)                               | ,       |
| `class`     | 記事リストのクラス名                                                               | post    |
| `amount`    | 表示する記事数(0 = 無制限)                                                         | 6       |
| `transform` | 記事名の表示を変更するための関数。[list_categories](#list-categories)の例を参照    |

### tagcloud

タグクラウドを挿入します。

```js
<%- tagcloud([tags], [options]) %>
```

| Option        | Description                                                                                                                                             | Default   |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `min_font`    | 最小フォントサイズ                                                                                                                                      | 10        |
| `max_font`    | 最大フォントサイズ                                                                                                                                      | 20        |
| `unit`        | フォントサイズの単位                                                                                                                                    | px        |
| `amount`      | タグの総数                                                                                                                                              | unlimited |
| `orderby`     | タグの並び順                                                                                                                                            | name      |
| `order`       | 並べ方。 昇順なら`1`または`asc`。降順なら`-1`または`desc`。                                                                                             | 1         |
| `color`       | タグクラウドをカラーにする                                                                                                                              | false     |
| `start_color` | 最初の色。(`#b700ff`)や rgba (`rgba(183, 0, 255, 1)`)、hsla (`hsla(283, 100%, 50%, 1)`)、[カラーキーワード] を使用可能。`color`が true の場合のみ有効。 |
| `end_color`   | 最後の色。(`#b700ff`)や rgba (`rgba(183, 0, 255, 1)`)、hsla (`hsla(283, 100%, 50%, 1)`)、[カラーキーワード] を使用可能。`color`が true の場合のみ有効。 |
| `class`       | タグのクラス名の接頭辞                                                                                                                                  |
| `level`       | 個別のクラス名の数。`class`が設定されている場合のみ有効。                                                                                               | 10        |

**例：**

```js
// デフォルトオプション
<%- tagcloud() %>

// タグの総数を30に制限
<%- tagcloud({amount: 30}) %>
```

## 様々なもの

### paginator

ページネーションを挿入します。

```js
<%- paginator(options) %>
```

| オプション  | 説明                                                                               | デフォルト値 |
| ----------- | ---------------------------------------------------------------------------------- | ------------ |
| `base`      | ベース URL                                                                         | /            |
| `format`    | URL フォーマット                                                                   | page/%d/     |
| `total`     | ページ数                                                                           | 1            |
| `current`   | 現在のページ数                                                                     | 0            |
| `prev_text` | The link text of previous page. Works only if `prev_next` is set to true.          | Prev         |
| `next_text` | The link text of next page. Works only if `prev_next` is set to true.              | Next         |
| `space`     | The space text                                                                     | &hellp;      |
| `prev_next` | Display previous and next links                                                    | true         |
| `end_size`  | The number of pages displayed on the start and the end side                        | 1            |
| `mid_size`  | The number of pages displayed between current page, but not including current page | 2            |
| `show_all`  | Display all pages. If this is set to true, `end_size` and `mid_size` will not work | false        |
| `escape`    | Escape HTML tags                                                                   | true         |

**Examples:**

```js
<%- paginator({
  prev_text: '<',
  next_text: '>'
}) %>
```

```html
<!-- Rendered as -->
<a href="/1/">&lt;</a>
<a href="/1/">1</a>
2
<a href="/3/">3</a>
<a href="/3/">&gt;</a>
```

```js
<%- paginator({
  prev_text: '<i class="fa fa-angle-left"></i>',
  next_text: '<i class="fa fa-angle-right"></i>',
  escape: false
}) %>
```

```html
<!-- Rendered as -->
<a href="/1/"><i class="fa fa-angle-left"></i></a>
<a href="/1/">1</a>
2
<a href="/3/">3</a>
<a href="/3/"><i class="fa fa-angle-right"></i></a>
```

### search_form

Inserts a Google search form.

```js
<%- search_form(options) %>
```

| Option   | Description                                                                                                               | Default     |
| -------- | ------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `class`  | The class name of form                                                                                                    | search-form |
| `text`   | Search hint word                                                                                                          | Search      |
| `button` | Display search button. The value can be a boolean or a string. If the value is a string, it'll be the text of the button. | false       |

### number_format

Formats a number.

```js
<%- number_format(number, [options]) %>
```

| Option      | Description                                                                 | Default |
| ----------- | --------------------------------------------------------------------------- | ------- |
| `precision` | The precision of number. The value can be `false` or a nonnegative integer. | false   |
| `delimiter` | The thousands delimiter                                                     | ,       |
| `separator` | The separator between the fractional and integer digits.                    | .       |

**Examples:**

```js
<%- number_format(12345.67, {precision: 1}) %>
// 12,345.68

<%- number_format(12345.67, {precision: 4}) %>
// 12,345.6700

<%- number_format(12345.67, {precision: 0}) %>
// 12,345

<%- number_format(12345.67, {delimiter: ''}) %>
// 12345.67

<%- number_format(12345.67, {separator: '/'}) %>
// 12,345/67
```

### meta_generator

Inserts [generator tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta).

```js
<%- meta_generator() %>
```

**Examples:**

```js
<%- meta_generator() %>
// <meta name="generator" content="Hexo 4.0.0">
```

### open_graph

Inserts [Open Graph] data.

```js
<%- open_graph([options]) %>
```

| Option         | Description                         | Default                                             |
| -------------- | ----------------------------------- | --------------------------------------------------- |
| `title`        | Page title (`og:title`)             | `page.title`                                        |
| `type`         | Page type (`og:type`)               | blog                                                |
| `url`          | Page URL (`og:url`)                 | `url`                                               |
| `image`        | Page images (`og:image`)            | All images in the content                           |
| `site_name`    | Site name (`og:site_name`)          | `config.title`                                      |
| `description`  | Page description (`og:description`) | Page excerpt or first 200 characters of the content |
| `twitter_card` | Twitter card type (`twitter:card`)  | summary                                             |
| `twitter_id`   | Twitter ID (`twitter:creator`)      |
| `twitter_site` | Twitter Site (`twitter:site`)       |
| `google_plus`  | Google+ profile link                |
| `fb_admins`    | Facebook admin ID                   |
| `fb_app_id`    | Facebook App ID                     |

### toc

Parses all heading tags (h1~h6) in the content and inserts a table of contents.

```js
<%- toc(str, [options]) %>
```

| Option        | Description                            | Default |
| ------------- | -------------------------------------- | ------- |
| `class`       | Class name                             | toc     |
| `list_number` | Displays list number                   | true    |
| `max_depth`   | Maximum heading depth of generated toc | 6       |
| `min_depth`   | Minimum heading depth of generated toc | 1       |

**Examples:**

```js
<%- toc(page.content) %>
```

[color keywords]: http://www.w3.org/TR/css3-color/#svg-color
[moment.js]: http://momentjs.com/
[open graph]: http://ogp.me/
