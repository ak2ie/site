---
title: 貢献
---

Hexo の開発への参加を歓迎しています。🤗

## 開発

Hexo の開発への参加を歓迎しています。このドキュメントは手順を進めるのに役立ちます。

### はじめる前に

はじめに、[Contributor Covenant Code of Conduct](https://github.com/hexojs/hexo/blob/master/CODE_OF_CONDUCT.md) を読んでください。

次のコーディングスタイルに従ってください：

- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)への準拠
- 空白 2 つでのソフトタブによるインデントの使用
- 行頭でのカンマ不使用

また、Hexo では独自の [ESLint 設定](https://github.com/hexojs/eslint-config-hexo)も使用しており、あなたの貢献によって ESLint が喜ぶようにしてください。

### 手順

1. [hexojs/hexo]を Fork します
2. 自分のコンピュータにリポジトリを Clone して、依存関係をインストールします

```bash
$ git clone https://github.com/<username>/hexo.git
$ cd hexo
$ npm install
$ git submodule update --init
```

3. feature ブランチを作成します

```bash
$ git checkout -b new_feature
```

4. 修正します
5. ブランチを Push します

```
$ git push origin new_feature
```

6. pull request を作成し、修正内容の説明を書きます

### 注意

- `package.json`内のバージョン番号を変更しないでください
- pull request はテストに合格した場合のみマージされます。提出前に忘れずにテストを実行してくだい。

```bash
$ npm test
```

## 公式プラグインの更新

[公式プラグイン](https://github.com/hexojs)への PR や isuue も歓迎しています。 🤗

## ドキュメントの更新

Hexo のドキュメントはオープンソースであり、ソースコードは [hexojs/site] にあります。

### 手順

1. [hexojs/site] を Fork します
2. 自分のコンピュータにリポジトリを Clone して、依存関係をインストールします

```bash
$ npm install hexo-cli -g # hexo-cli をインストールしていない場合
$ git clone https://github.com/<username>/site.git
$ cd site
$ npm install
```

3. ドキュメントを修正します。サーバーを実行するとプレビューできます。

```bash
$ hexo server
```

4. ブランチを Push します
5. pull request を作成し、修正内容の説明を書きます

### 翻訳

1. `source`フォルダ内に新しい言語のフォルダを作成します（全て小文字）
2. `source` フォルダ内の Markdown とテンプレートファイルを新しい言語のフォルダにコピーします
3. `source/_data/language.yml`に新しい言語を追加します
4. `themes/navy/languages` 内の `en.yml` をコピーして名前を言語名に変更します（全て小文字）

## 問題を報告

Hexo を使用する中で問題が発生したら、[トラブルシューティング](troubleshooting.html) で解決策を探すか、[GitHub](https://github.com/hexojs/hexo/issues) または [Google Group](https://groups.google.com/group/hexo)で質問してください。答えが見つからなかったら、GitHub に報告してください。

1. [デバッグモード](commands.html#デバッグモード)で問題を再現させる
2. GitHub で新しい issue を提出する際の issue テンプレートに従って、デバッグメッセージとバージョンを記載する

[hexojs/hexo]: https://github.com/hexojs/hexo
[hexojs/site]: https://github.com/hexojs/site
