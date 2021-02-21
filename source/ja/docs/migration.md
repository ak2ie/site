---
title: マイングレーション
---

## RSS

はじめに、`hexo-migrator-rss` プラグインをインストールしてください。

```bash
$ npm install hexo-migrator-rss --save
```

プラグインをインストールしたら、RSS から全ての記事をマイングレーションするために、次のコマンドを実行します。`source` にはファイルパスまたは URL を指定できます。

```bash
$ hexo migrate rss <source>
```

## Jekyll

Jekyll の`_posts`フォルダ内の全てファイルを`source/_posts`フォルダに移動します。

`_config.yml`内の`new_post_name`設定を変更します：

```yaml
new_post_name: :year-:month-:day-:title.md
```

## Octopress

Octopress の`source/_posts`フォルダ内の全てのファイルを`source/_posts`に移動します。

`_config.yml`内の`new_post_name`設定を変更します。

```yaml
new_post_name: :year-:month-:day-:title.md
```

## WordPress

はじめに、`hexo-migrator-wordpress`プラグインをインストールします。

```bash
$ npm install hexo-migrator-wordpress --save
```

WordPress ダッシュボードの「ツール」→「エクスポート」→「ワードプレス」の順に進んで、WordPress サイトをエクスポートします。（詳細は[WordPress サポートページ](https://wordpress.com/ja/support/export/)参照。）

つぎに実行：

```bash
$ hexo migrate wordpress <source>
```

`source`には WordPress のエクスポートファイルパスまたは URL を指定できます。

## Joomla

はじめに、`hexo-migrator-joomla`をインストールします。

```bash
$ npm install hexo-migrator-joomla --save
```

[J2XML](http://extensions.joomla.org/extensions/migration-a-conversion/data-import-a-export/12816?qh=YToxOntpOjA7czo1OiJqMnhtbCI7fQ%3D%3D)コンポーネントを使って、Joomla の記事をエクスポートします。

つぎに実行：

```bash
$ hexo migrate joomla <source>
```

`source`には Joomla のエクスポートファイルパスまたは URL を指定できます。
