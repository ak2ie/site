---
title: セットアップ
---

{% youtube 0m2HnATkHOk %}

Hexo をインストールしたら、対象のフォルダ（`<folder>`）内で Hexo を初期化するために次のコマンドを実行します。

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

初期化すると、プロジェクトフォルダはこのようになります：

```plain
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### \_config.yml

サイトの [設定](configuration.html) ファイルです。ほとんどの設定はここで変更できます。

### package.json

アプリケーションデータです。デフォルトで、[EJS](https://ejs.co/)、[Stylus](http://learnboost.github.io/stylus/)、[Markdown](http://daringfireball.net/projects/markdown/)レンダラーがインストールされています。後からアンインストールすることもできます。

```json package.json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.8.0",
    "hexo-generator-archive": "^0.1.5",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.1",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-renderer-marked": "^0.3.2",
    "hexo-server": "^0.3.3"
  }
}
```

### scaffolds

[ひな形](writing.html#Scaffolds) フォルダです。新しい記事を作成するとき、Hexo はひな形に基づいた新しいファイルを作成します。

### source

ソースフォルダです。ここはサイトのコンテンツを格納する場所です。Hexo は隠しファイルとフォルダ、先頭が`_`（アンダースコア）始まる名前のファイルとフォルダを無視します。（`_posts`フォルダを除く）レンダリングするファイル（例：Markdown、HTML）は処理されて`public`フォルダに格納され、他のファイルは単純にコピーされます。

### themes

[テーマ](themes.html) フォルダです。Hexo はサイトのコンテンツとテーマを組み合わせて静的ウェブサイトを生成します。
