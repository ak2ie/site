---
title: コマンド
---

## init

```bash
$ hexo init [folder]
```

Initializes a website. If no `folder` is provided, Hexo will set up a website in the current directory.

This command is a shortcut that runs the following steps:

1. Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) including [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape) into the current directory or a target folder if specified.
2. Install dependencies using a package manager: [Yarn 1](https://classic.yarnpkg.com/lang/en/), [pnpm](https://pnpm.js.org) or [npm](https://docs.npmjs.com/cli/install), whichever is installed; if there are more than one installed, the priority is as listed. npm is bundled with [Node.js](/docs/#Install-Node-js) by default.

## init

```bash
$ hexo init [folder]
```

ウェブサイトを初期化します。`folder`を指定しない場合、Hexo はカレントディレクトリにウェブサイトをセットアップします。

このコマンドは次の手順を実行するショートカットです：

1. [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape)を含む[hexo-starter](https://github.com/hexojs/hexo-starter)をカレントディレクトリまたは指定したフォルダに Git clone します。
2. パッケージマネージャを使用して依存モジュールをインストールします: [Yarn 1](https://classic.yarnpkg.com/lang/en/) や [pnpm](https://pnpm.js.org) 、[npm](https://docs.npmjs.com/cli/install)のいずれかインストールされたものです。複数インストールされている場合、優先順位は記載の通りです。npm は[Node.js](/docs/#Install-Node-js)によってデフォルトでバンドルされています。

## new

```bash
$ hexo new [layout] <title>
```

Creates a new article. If no `layout` is provided, Hexo will use the `default_layout` from [\_config.yml](configuration.html). If the `title` contains spaces, surround it with quotation marks.

| Option            | Description                                |
| ----------------- | ------------------------------------------ |
| `-p`, `--path`    | Post path. Customize the path of the post. |
| `-r`, `--replace` | Replace the current post if existed.       |
| `-s`, `--slug`    | Post slug. Customize the URL of the post.  |

By default, Hexo will use the title to define the path of the file. For pages, it will create a directory of that name and an `index.md` file in it. Use the `--path` option to override that behaviour and define the file path:

```bash
hexo new page --path about/me "About me"
```

will create `source/about/me.md` file with the title "About me" set in the front matter.

Please note that the title is mandatory. For example, this will not result in the behaviour you might expect:

```bash
hexo new page --path about/me
```

will create the post `source/_posts/about/me.md` with the title "page" in the front matter. This is because there is only one argument (`page`) and the default layout is `post`.

## new

```bash
$ hexo new [layout] <title>
```

新しい記事を作成します。`layout`を指定しない場合、Hexo は[\_config.yml](configuration.html)の`default_layout`を使用します。`title`に空白を含む場合、引用符で囲んでください。

| オプション        | 説明                                      |
| ----------------- | ----------------------------------------- |
| `-p`, `--path`    | 記事のパス。記事のパスを変更します。      |
| `-r`, `--replace` | 既存の記事を置換します。                  |
| `-s`, `--slug`    | 記事のスラッグ。記事の URL を変更します。 |

デフォルトでは、Hexo はファイルのパスをタイトルに使用します。ページの場合、その名前のディレクトリと `index.md` ファイルが作成されます。この動作を変更してファイルのパスを定義するには、`--path` オプションを使用します：：

```bash
hexo new page --path about/me "About me"
```

will create `source/about/me.md` file with the title "About me" set in the front matter.

Please note that the title is mandatory. For example, this will not result in the behaviour you might expect:

```bash
hexo new page --path about/me
```

will create the post `source/_posts/about/me.md` with the title "page" in the front matter. This is because there is only one argument (`page`) and the default layout is `post`.

## generate

```bash
$ hexo generate
```

Generates static files.

| Option                | Description                                                              |
| --------------------- | ------------------------------------------------------------------------ |
| `-d`, `--deploy`      | Deploy after generation finishes                                         |
| `-w`, `--watch`       | Watch file changes                                                       |
| `-b`, `--bail`        | Raise an error if any unhandled exception is thrown during generation    |
| `-f`, `--force`       | Force regenerate                                                         |
| `-c`, `--concurrency` | Maximum number of files to be generated in parallel. Default is infinity |

## publish

```bash
$ hexo publish [layout] <filename>
```

Publishes a draft.

## publish

```bash
$ hexo publish [layout] <filename>
```

ドラフト版を出力します。

## server

```bash
$ hexo server
```

Starts a local server. By default, this is at `http://localhost:4000/`.

| Option           | Description                            |
| ---------------- | -------------------------------------- |
| `-p`, `--port`   | Override default port                  |
| `-s`, `--static` | Only serve static files                |
| `-l`, `--log`    | Enable logger. Override logger format. |

## server

```bash
$ hexo server
```

ローカルサーバーを起動します。デフォルトでは、`http://localhost:4000/`です。

| オプション       | 説明                                 |
| ---------------- | ------------------------------------ |
| `-p`, `--port`   | デフォルトポートを変更               |
| `-s`, `--static` | 静的ファイルのみを配信               |
| `-l`, `--log`    | ログを有効化。ログフォーマットを変更 |

## deploy

```bash
$ hexo deploy
```

ウェブサイトを公開します。

| オプション         | 説明         |
| ------------------ | ------------ |
| `-g`, `--generate` | 公開前に生成 |

## render

```bash
$ hexo render <file1> [file2] ...
```

Renders files.

| Option           | Description        |
| ---------------- | ------------------ |
| `-o`, `--output` | Output destination |

## migrate

```bash
$ hexo migrate <type>
```

[Migrates](migration.html) content from other blog systems.

## clean

```bash
$ hexo clean
```

Cleans the cache file (`db.json`) and generated files (`public`).

## list

```bash
$ hexo list <type>
```

Lists all routes.

## version

```bash
$ hexo version
```

バージョン情報を表示します。

## Options

### Safe mode

```bash
$ hexo --safe
```

Disables loading plugins and scripts. Try this if you encounter problems after installing a new plugin.

### Debug mode

```bash
$ hexo --debug
```

Logs verbose messages to the terminal and to `debug.log`. Try this if you encounter any problems with Hexo. If you see errors, please [raise a GitHub issue](https://github.com/hexojs/hexo/issues/new).

### Silent mode

```bash
$ hexo --silent
```

Silences output to the terminal.

### Customize config file path

```bash
$ hexo --config custom.yml
```

Uses a custom config file (instead of `_config.yml`). Also accepts a comma-separated list (no spaces) of JSON or YAML config files that will combine the files into a single `_multiconfig.yml`.

```bash
$ hexo --config custom.yml,custom2.json
```

### Display drafts

```bash
$ hexo --draft
```

Displays draft posts (stored in the `source/_drafts` folder).

### Customize CWD

```bash
$ hexo --cwd /path/to/cwd
```

Customizes the path of current working directory.
