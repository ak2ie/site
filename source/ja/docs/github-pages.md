---
title: GitHub ページ
---

このチュートリアルでは、GitHub ページに公開するために[GitHub Actions](https://docs.github.com/ja/actions)を使用します。パブリックリポジトリとプライベートリポジトリ両方で動作します。GitHub にソースフォルダをアップロードしたくない場合は、[1 コマンドでの公開](#One-command-deployment)に進んでください。

1. <b>_ユーザー名_.github.io</b>（「ユーザー名」は GitHub のユーザー名）リポジトリを作成します。他のリポジトリをアップロード済の場合は、代わりに名前を変更します。
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

3. リポジトリの **`source` branch** に Hexo フォルダのファイルを Push します。デフォルトでは`public/`フォルダはアップロードされず（すべきではありません）、`.gitignore`ファイルには`public/`の行があります。フォルダ構成は`.gitmodules`ファイルを除き[このリポジトリ](https://github.com/hexojs/hexo-starter)とほぼ同じはずです。

- `source` を GitHub に Push します：

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

5. 公開が完了すると、リポジトリの`master`ブランチにページが生成されます。
6. GitHub のリポジトリ設定を開き、"GitHub Pages" セクションに進みソースを **master branch**に変更します。
7. _ユーザー名_.github.io でページを確認します。

注意 - `CNAME`でカスタムドメインを指定している場合は、`CNAME`ファイルに`source/`フォルダを追加する必要があります。

## プロジェクトページ

GitHub でプロジェクトページを使用したい場合：

1. GitHub のリポジトリに移動します。**Settings**タブを開きます。Change the **Repository name** so your blog is available at <b>username.github.io/_repository_</b>, **repository** は*blog* または _hexo_ のようにどんな名前でも構いません。
2. **\_config.yml** を編集し、change the `root:` value to the `/<repository>/` (先頭と末尾はスラッシュである必要があり、).
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

5. Once the deployment is finished, the generated pages can be found in the `gh-pages` branch of your repository
6. In your GitHub repo's setting, navigate to "GitHub Pages" section and change Source to **gh-pages branch**.

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
4. _ユーザー名_.github.io を確認します。

## 参考リンク

- [GitHub Pages](https://help.github.com/categories/github-pages-basics/)
- [Travis CI Docs](https://docs.travis-ci.com/user/tutorial/)
- [peaceiris/actions-gh-pages](https://github.com/marketplace/actions/github-pages-action)
