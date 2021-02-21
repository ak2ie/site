---
title: GitLab Pages
---

1. <b>_ユーザー名_.gitlab.io</b>という名前で新しいリポジトリを作成します。ユーザー名は GitLab のユーザー名です。すでに他のリポジトリをアップロード済の場合は、代わりに名前を変更します。
2. `Settings -> CI / CD -> Shared Runners`から Shared Runners を有効化します。
3. Hexo フォルダ内のファイルをリポジトリにプッシュします。デフォルトでは`public/`フォルダはアップロードされず（すべきではありません）、`.gitignore`に`public/`の行があることを確認してください。フォルダ構成は[このリポジトリ](https://gitlab.com/pages/hexo)とほぼ同じはずです。
4. 次の内容で`.gitlab-ci.yml`ファイルを(\_config.yml と package.json も一緒に)リポジトリに追加します。

```yml
image: node:10-alpine # nodejs v10 LTS を使用
cache:
  paths:
    - node_modules/

before_script:
  - npm install hexo-cli -g
  - npm install

pages:
  script:
    - hexo generate
  artifacts:
    paths:
      - public
  only:
    - master
```

5. GitLab CI のデプロイジョブが完了すると、_ユーザー名_.gitlab.io が動いているはずです。
6. (オプション) 生成されたサイトのアセット(html、css、js など)を解析したい場合は、[job artifact](https://docs.gitlab.com/ee/user/project/pipelines/job_artifacts.html)で確認できます。

## プロジェクトページ

GitLab でプロジェクトページを使用したい場合：

1. `Settings -> General -> Advanced -> Change path`を開きます。ウェブサイトが配信される<b>username.gitlab.io/_名前_</b>の名前に設定する値を変更します。*blog*　や *hexo*のようにどんな名前でも構いません。
2. **\_config.yml**を編集し、`root:` の値を`""` から `"名前"`に変更します。
3. コミットしてプッシュします。

## 参考リンク

- [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/index.html)
- [GitLab CI Docs](https://docs.gitlab.com/ee/ci/README.html)
