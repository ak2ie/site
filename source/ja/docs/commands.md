---
title: コマンド
---

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

新しい記事を作成します。`layout`を指定しない場合、Hexo は[\_config.yml](configuration.html)の`default_layout`を使用します。`title`に空白を含む場合、引用符で囲んでください。

| オプション        | 説明                                      |
| ----------------- | ----------------------------------------- |
| `-p`, `--path`    | 記事のパス。記事のパスを変更します。      |
| `-r`, `--replace` | 既存の記事を置換します。                  |
| `-s`, `--slug`    | 記事のスラッグ。記事の URL を変更します。 |

デフォルトでは、Hexo はファイルのパスをタイトルに使用します。ページの場合、その名前のディレクトリ内に `index.md` ファイルが作成されます。この動作を変更してファイルパス指定するには、`--path` オプションを使用します：：

```bash
hexo new page --path about/me "About me"
```

これで、"About me"というタイトルが設定された`source/about/me.md`ファイルが作成されます。

タイトルは必須であることに注意してください。例えば、次の実行結果は想定外かもしれません：

```bash
hexo new page --path about/me
```

「page」というタイトルの `source/_posts/about/me.md`ファイルが作成されます。これは、1 つの引数（`page`）のみが指定され、デフォルトレイアウトが`post`であるためです。

## generate

```bash
$ hexo generate
```

静的ファイルを生成します。

| オプション            | 説明                                               |
| --------------------- | -------------------------------------------------- |
| `-d`, `--deploy`      | 生成完了後に公開                                   |
| `-w`, `--watch`       | ファイルの変更を監視                               |
| `-b`, `--bail`        | 生成時に想定外の例外が発生した場合にエラーを投げる |
| `-f`, `--force`       | 強制的に再生成                                     |
| `-c`, `--concurrency` | 並列に生成するファイルの最大値。デフォルトは無限。 |

## publish

```bash
$ hexo publish [layout] <filename>
```

下書きを公開します。

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

ファイルを描画します。

| オプション       | 説明   |
| ---------------- | ------ |
| `-o`, `--output` | 出力先 |

## migrate

```bash
$ hexo migrate <type>
```

他のブログシステムから[マイングレーション](migration.html)します。

## clean

```bash
$ hexo clean
```

キャッシュファイル(`db.json`)と生成ファイル(`public`)を消去します。

## list

```bash
$ hexo list <type>
```

全てのルートを表示します。

## version

```bash
$ hexo version
```

バージョン情報を表示します。

## オプション

### セーフモード

```bash
$ hexo --safe
```

プラグインとスクリプトの読み込みを無効化します。新しいプラグインをインストール後に問題が発生した場合に試してください。

### デバッグモード

```bash
$ hexo --debug
```

ターミナル画面と`debug.log`に、詳細なメッセージを出力します。Hexo に何らかの問題が発生した場合に試してください。エラーを発見したら、[GitHub に issue を投稿](https://github.com/hexojs/hexo/issues/new).してください。

### サイレントモード

```bash
$ hexo --silent
```

ターミナル画面への出力を無効にします。

### 設定ファイルパスの変更

```bash
$ hexo --config custom.yml
```

任意の設定ファイル（`_config.yml`の代替）を使用できます。JSON または YAML 設定ファイルを、カンマ区切り（空白なし）でつなげて指定すると、1 つの`_multiconfig.yml`ファイルに統合されます。

```bash
$ hexo --config custom.yml,custom2.json
```

### 下書きの表示

```bash
$ hexo --draft
```

下書き(`source/_drafts`フォルダに格納)を表示します。

### CWD の変更

```bash
$ hexo --cwd /path/to/cwd
```

カレントワーキングディレクトリ(current working directory)のパスを変更します。
