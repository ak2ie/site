---
title: 設定
---

`_config.yml`または[代替設定ファイル](#Using-an-Alternate-Config)でサイトの設定を変更できます。

### サイト

| 項目          | 説明                                                                                                                                                                                                                                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`       | ウェブサイトのタイトル                                                                                                                                                                                                                            |
| `subtitle`    | ウェブサイトのサブタイトル                                                                                                                                                                                                                        |
| `description` | ウェブサイトの説明                                                                                                                                                                                                                                |
| `keywords`    | ウェブサイトのキーワード。複数設定可能。                                                                                                                                                                                                          |
| `author`      | あなたの名前                                                                                                                                                                                                                                      |
| `language`    | ウェブサイトの言語。[2 文字の ISO-639-1 コード](https://ja.wikipedia.org/wiki/ISO_639-1%E3%82%B3%E3%83%BC%E3%83%89%E4%B8%80%E8%A6%A7) または [その異種](/docs/internationalization)を使用してください。デフォルトは`en`です。                     |
| `timezone`    | ウェブサイトのタイムゾーン。Hexo はコンピュータのデフォルト設定値を使用します。利用可能なタイムゾーンの一覧は[ここ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)にあります。例えば、`America/New_York`や`Japan`、`UTC`などです。 |

### URL

| 項目                         | 説明                                                                            | デフォルト値                |
| ---------------------------- | ------------------------------------------------------------------------------- | --------------------------- |
| `url`                        | ウェブサイトの URL。必ず`http://` または `https://` から始める必要があります。  |
| `root`                       | ウェブサイトのルートディレクトリ                                                |
| `permalink`                  | 記事の[パーマリンク](permalinks.html) のフォーマット                            | `:year/:month/:day/:title/` |
| `permalink_defaults`         | パーマリンクの各項目のデフォルト値                                              |
| `pretty_urls`                | [`permalink`](variables.html) 変数をきれいな URL に置換                         |
| `pretty_urls.trailing_index` | `false`に設定すると、末尾の`index.html`を除去                                   | `true`                      |
| `pretty_urls.trailing_html`  | `false`に設定すると、末尾の`.html`を除去 (_`index.html`除去には反映されません_) | `true`                      |

{% note info サブディレクトリでのウェブサイト作成 %}
ウェブサイトがサブディレクトリにある場合は(`http://example.org/blog`のようなとき)、`url` に `http://example.org/blog` を設定し、 `root` に `/blog/`を設定してください。
{% endnote %}

例:

```yaml
# 例えば、page.permalink が http://example.com/foo/bar/index.html の場合
pretty_urls:
  trailing_index: false
# このように設定すると、http://example.com/foo/bar/ になります。
```

### ディレクトリ

| 項目           | 説明                                                                                                                                               | デフォルト値     |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| `source_dir`   | ソースフォルダ。記事などが格納された場所。                                                                                                         | `source`         |
| `public_dir`   | 公開フォルダ。生成された静的ファイルが格納された場所。                                                                                             | `public`         |
| `tag_dir`      | タグディレクトリ                                                                                                                                   | `tags`           |
| `archive_dir`  | アーカイブディレクトリ                                                                                                                             | `archives`       |
| `category_dir` | カテゴリディレクトリ                                                                                                                               | `categories`     |
| `code_dir`     | コードディレクトリ ( `source_dir`のサブディレクトリ)                                                                                               | `downloads/code` |
| `i18n_dir`     | 多言語対応ディレクトリ                                                                                                                             | `:lang`          |
| `skip_render`  | 描画せずに、そのまま`public`フォルダにコピーするパス。[glob](https://github.com/micromatch/micromatch#extended-globbing)をパス指定に使用できます。 |

例：

```yaml
skip_render: "mypage/**/*"
# と指定すると、`source/mypage/index.html` と `source/mypage/code.js` は変更されずそのまま出力されます。

## これは記事の除外にも利用でき、
skip_render: "_posts/test-post.md"
# と指定すると、`source/_posts/test-post.md`は無視されます。
```

### 執筆

| 項目                    | 説明                                                                                                               | デフォルト値 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------ |
| `new_post_name`         | 新しい記事のファイル名フォーマット                                                                                 | `:title.md`  |
| `default_layout`        | デフォルトレイアウト名                                                                                             | `post`       |
| `titlecase`             | タイトルケース（前置詞・冠詞以外の先頭を大文字化）に変換するか                                                     | `false`      |
| `external_link`         | リンクを新しいタブで開くか                                                                                         |
| `external_link.enable`  | リンクを新しいタブで開くか                                                                                         | `true`       |
| `external_link.field`   | `site` 全体または `post`のみに適用するか                                                                           | `site`       |
| `external_link.exclude` | 除外するホスト名。`www`を含め、サブドメインを指定してください。                                                    | `[]`         |
| `filename_case`         | `1`ならファイル名を小文字に、`2`なら大文字に変換する                                                               | `0`          |
| `render_drafts`         | 下書きの表示有無                                                                                                   | `false`      |
| `post_asset_folder`     | [アセットフォルダ](asset-folders.html)を有効化するか                                                               | `false`      |
| `relative_link`         | リンクをルートフォルダからの相対パスにするか                                                                       | `false`      |
| `future`                | 未来の記事の表示有無                                                                                               | `true`       |
| `highlight`             | コードブロックのシンタックスハイライトの設定。使用方法は [Highlight.js](/docs/syntax-highlight#Highlight-js)参照。 |
| `prismjs`               | コードブロックのシンタックスハイライトの設定。使用方法は [PrismJS](/docs/syntax-highlight#PrismJS) 参照。          |

### ホームページ設定

| 項目                             | 設定                                                                                                   | デフォルト値 |
| -------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------ |
| `index_generator`                | 記事のアーカイブを生成。[hexo-generator-index](https://github.com/hexojs/hexo-generator-index)を使用。 |
| `index_generator.path`           | ブログのインデックスページのルートパス                                                                 | `''`         |
| `index_generator.per_page`       | 1 ページに表示する記事数                                                                               | `10`         |
| `index_generator.order_by`       | 記事の表示順。デフォルト値は日付の降順（新しいものから古いもの）                                       | `-date`      |
| `index_generator.pagination_dir` | URL フォーマット。[Pagination](#ページネーション)設定を参照。                                          | `page`       |

### カテゴリとタグ

| 項目               | 説明               | デフォルト値    |
| ------------------ | ------------------ | --------------- |
| `default_category` | デフォルトカテゴリ | `uncategorized` |
| `category_map`     | カテゴリスラッグ   |
| `tag_map`          | タグスラッグ       |

### 日付・時刻フォーマット

Hexo は日付処理に[Moment.js](http://momentjs.com/) を使用します。

| 項目             | 説明                                                                           | デフォルト値 |
| ---------------- | ------------------------------------------------------------------------------ | ------------ |
| `date_format`    | 日付フォーマット                                                               | `YYYY-MM-DD` |
| `time_format`    | 時刻フォーマット                                                               | `HH:mm:ss`   |
| `updated_option` | [`updated`](/docs/variables#Page-Variables) の値が表題で指定されない場合に使用 | `mtime`      |

{% note info updated_option %}
`updated_option` は表題で `updated`が指定されない場合に使用されます。

- `mtime`：ファイルの変更日時を`updated`に設定します。Hexo 3.0.0 からのデフォルトの仕様です。
- `date`：`date` の値を `updated`に設定します。通常、ファイルの変更日時が実際と異なる Git ワークフローで使用されます。
- `empty`：未指定の場合、単純に`updated`を設定しません。ほとんどのテーマやプラグインでは対応していません。

`use_date_for_updated`は非推奨で、次のメジャーバージョンでは削除予定です。代わりに`updated_option: 'date'`を使用してください。
{% endnote %}

### ページネーション

| 項目             | 説明                                                                 | デフォルト値 |
| ---------------- | -------------------------------------------------------------------- | ------------ |
| `per_page`       | 1 ページに表示する記事数 。`0`を設定するとページネーションを無効化。 | `10`         |
| `pagination_dir` | URL フォーマット                                                     | `page`       |

例:

```yaml
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/awesome-page/2
```

### 拡張機能

| 項目             | 説明                                                                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `theme`          | テーマ名。`false`を設定するとテーマを無効化。                                                                                               |
| `theme_config`   | テーマの設定。テーマのデフォルト値を上書きする場合、このキーの配下に設定してください。値                                                    |
| `deploy`         | 公開時の設定                                                                                                                                |
| `meta_generator` | [Meta generator](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes) タグ。`false`を設定すると、タグの挿入を無効化。 |

### ファイルやフォルダの取込と除外

特定のファイル・フォルダを明示的に処理するか・無視するには明示的に処理するか無視するには次のオプションを使用します。[glob expressions](https://github.com/micromatch/micromatch#extended-globbing)によるパス指定に対応しています。

`include` と `exclude` オプションは `source/` フォルダにのみ適用されますが、`ignore`オプションは全てのフォルダに適用されます。

| 項目      | 説明                                                                                    |
| --------- | --------------------------------------------------------------------------------------- |
| `include` | 隠しファイルを含める (アンダースコアと、\*以外から始まる名前のファイル・フォルダを含む) |
| `exclude` | 除外するファイル・フォルダ                                                              |
| `ignore`  | 無視するファイル・フォルダ                                                              |

例：

```yaml
# 取込または除外するファイル・フォルダ
include:
  - ".nojekyll"
  # 'source/css/_typing.css'を取込む
  - "css/_typing.css"
  # 'source/_css/'フォルダ内の全ファイルを取込む
  - "_css/*"
  # 'source/_css/'フォルダ内とサブフォルダ内の全ファイルを取込む
  - "_css/**/*"

exclude:
  # 'source/js/test.js'を除外
  - "js/test.js"
  # 'source/js/'内の全ファイルを除外
  - "js/*"
  # 'source/js/'内とサブフォルダ内の全ファイルを除外
  - "js/**/*"
  # 'source/js/'内の'test'から始まるファイル名の全ファイルを除外
  - "js/test*"
  # 'source/js/'内とサブフォルダ内の'test'から始まるファイル名の全ファイルを除外
  - "js/**/test*"
  # 'source/_posts/'内の記事を除外するために使用しないでください。
  # そのためには skip_render を使用してください。または、ファイル名の先頭にアンダースコアを付けてください。
  # - "_posts/hello-world.md" # これはうまく動きません。

ignore:
  # 'foo'という名前の全フォルダを無視
  - "**/foo"
  # 'themes/' フォルダ内の 'foo' フォルダのみを無視
  - "**/themes/*/foo"
  # 上記と同じですが、'themes/'の各サブフォルダにも適用
  - "**/themes/**/foo"
```

リストの各値はシングル/ダブルクオーテーションで囲む必要があります。

`include:` と `exclude:` は `themes/` フォルダには適用されません。`ignore:` を使うか、代わりにファイル/フォルダ名の先頭にアンダースコアを付けて除外してください。

\* `source/_posts`は例外ですが、アンダースコアから始まる名前のファイル・フォルダは無視されます。`include:`ルールをそのフォルダ内で使用するのは推奨しません。

### 代替設定の使用

`hexo`コマンドに `--config`フラグで YAML または JSON 設定ファイルや、カンマ区切り（空白なし）で複数の YAML または JSON ファイルパスのリストを付与すると、カスタム設定ファイルを指定できます。

```bash
# '_config.yml'の代わりに'custom.yml'を使用します
$ hexo server --config custom.yml

# 'custom.yml' と 'custom2.json' を使用しますが、'custom2.json'を優先します
$ hexo server --config custom.yml,custom2.json
```

複数のファイルを使用すると、全ての設定ファイルは統合され設定は`_multiconfig.yml`にマージされて保存されます。後の値が優先されます。これはどんなに深いオブジェクトの JSON や YAML ファイルでも処理されます。**リストに空白は許容されない**ことに注意してください。

例えば、上記の例として`custom.yml`に`foo: bar`があり、`custom2.json`に`"foo": "dinosaur"`があった場合、`_multiconfig.yml`には `foo: dinosaur`が出力されます。

### 代替テーマ設定

Hexo のテーマは独立したプロジェクトで、`_config.yml`ファイルによって分割されます。

テーマをフォークして、自分の設定を含むカスタムバージョンを管理する代わりに、別の方法で設定することができます：

**サイトのプライマリ設定ファイル`theme_config`から**

> Hexo 2.8.2 から対応

```yml
# _config.yml
theme: "my-theme"
theme_config:
  bio: "My awesome bio"
  foo:
    bar: "a"
```

```yml
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

結果としてテーマ設定はこのようになります：

```json
{
  "bio": "My awesome bio",
  "logo": "a-cool-image.png",
  "foo": {
    "bar": "a",
    "baz": "b"
  }
}
```

**専用の`_config.[theme].yml`ファイルから**

> Hexo 5.0.0 から対応

サイトフォルダ内に格納された`yml` と `json` ファイル両方に対応しています。 `_config.yml`内の`theme`は、Hexo が `_config.[theme].yml`を読み込むために、必ず設定しなければいけません。

```yml
# _config.yml
theme: "my-theme"
```

```yml
# _config.my-theme.yml
bio: "My awesome bio"
foo:
  bar: "a"
```

```yml
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

結果としてテーマ設定はこのようになります：

```json
{
  "bio": "My awesome bio",
  "logo": "a-cool-image.png",
  "foo": {
    "bar": "a",
    "baz": "b"
  }
}
```

{% note %}
テーマ設定は 1 つの場所に格納することを強く推奨します。しかし、テーマ設定を分割して格納する必要がある場合は、設定の優先順位を気にとめておいてください：サイトのプライマリ設定ファイル内の`theme_config`は、マージ時の優先度が最も高く、テーマ専用の設定ファイルよりも優先されます。テーマディレクトリ配下の`_config.yml`ファイルの優先度は最も低くなります。
{% endnote %}
