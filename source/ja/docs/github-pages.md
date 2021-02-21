---
title: GitHub ページ
---

このチュートリアルでは、GitHub ページに公開するために[GitHub Actions](https://docs.github.com/ja/actions)を使用します。パブリックリポジトリとプライベートリポジトリ両方で動作します。GitHub にソースフォルダをアップロードしたくない場合は、[1 コマンドでの公開](#One-command-deployment)に進んでください。

1. <b>_ユーザー名_.github.io</b>（「ユーザー名」は GitHub のユーザー名）リポジトリを作成します。すでに他のリポジトリをアップロード済の場合は、代わりに名前を変更します。
2. 次の _強調された_ 行を `package.json`に追加します： (すでに存在する場合はスキップしてください)

{% codeblock lang:json mark:2-4 %}
{
"scripts": {
"build": "hexo generate"
},
"hexo": {
"version": "5.0.0"
},
"dependencies": {
"hexo": "^5.0.0",
...
}
}
{% endcodeblock %}

3. リポジトリの **`source` ブランチ** に Hexo フォルダ内のファイルをプッシュします。デフォルトでは`public/`フォルダはアップロードされず（すべきではありません）、`.gitignore`ファイルに`public/`の行があることを確認してください。フォルダ構成は`.gitmodules`ファイルを除き[このリポジトリ](https://github.com/hexojs/hexo-starter)とほぼ同じはずです。

- `source` を GitHub にプッシュします：

```
$ git push origin source
```

4. 次の内容で`.github/workflows/pages.yml` ファイルを追加します：

```yml .github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
      - source # デフォルトブランチ

jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 12.x
        uses: actions/setup-node@v1
        with:
          node-version: "12.x"
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: master # 公開ブランチ
```

5. デプロイが完了すると、リポジトリの`master`ブランチにページが生成されます。
6. GitHub リポジトリの設定で、"GitHub Pages"セクションに進み、Source を**master ブランチ**に変更します。
7. _ユーザー名_.github.io でページを確認します。

注意 - `CNAME`でカスタムドメインを指定している場合は、`source/`フォルダに`CNAME`ファイルにを追加する必要があります。

## プロジェクトページ

GitHub でプロジェクトページを使用したい場合：

1. GitHub のリポジトリに移動します。**Settings**タブを開きます。ブログは<b>ユーザー名.github.io/_リポジトリ名_</b>で利用可能になるため、**リポジトリ名** を変更します。_blog_ または _hexo_ のようにどんな名前でも構いません。
2. **\_config.yml** を編集し、`root:` の値を `/<repository>/` に変更します。 (先頭と末尾はスラッシュである必要があり、括弧は除きます).
3. `.github/workflows/pages.yml`を次のように書き換えます。

```diff .github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
-      - source  # デフォルトブランチ
+      - master

jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
-          publish_branch: master  # 公開ブランチ
+          publish_branch: gh-pages
```

4. **`master` ブランチ**にコミット、プッシュします。

- GitHub の`master`ブランチへのプッシュ

```
$ git push origin master
```

5. デプロイが完了したら、リポジトリの `gh-pages` ブランチに生成されたファイルがあります。
6. GitHub リポジトリの設定で、"GitHub Pages"セクションに進み、Source を**gh-pages ブランチ**に変更します。

## 1 コマンドでの公開

次の説明は [1 コマンドでの公開](/docs/one-command-deployment) ページを参考にしています。

1. [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)をインストールします。
2. **\_config.yml**に次の設定を追加します。 (既存の内容は全て削除)

```yml
deploy:
  type: git
  repo: https://github.com/<ユーザー名>/<プロジェクト>
  # 例えば、https://github.com/hexojs/hexojs.github.io です。
  branch: gh-pages
```

3. `hexo clean && hexo deploy`を実行します。
4. _ユーザー名_.github.io でページを確認します。

## 参考リンク

- [GitHub Pages](https://help.github.com/categories/github-pages-basics/)
- [Travis CI Docs](https://docs.travis-ci.com/user/tutorial/)
- [peaceiris/actions-gh-pages](https://github.com/marketplace/actions/github-pages-action)
