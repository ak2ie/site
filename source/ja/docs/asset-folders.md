---
title: アセットフォルダ
---

## グローバル アセット フォルダ

アセット（添付ファイル）は画像や CSS、JavaScript ファイルのような`source`フォルダ内の記事以外のファイルです。例えば、Hexo プロジェクトに画像を配置したいなら、`source/images`ディレクトリに格納するのが一番簡単な方法です。こうすると、それらの画像は`![](/images/image.jpg)`で使用できます。

## 記事 アセット フォルダ

{% youtube feIDVQ2tz0o %}

画像とそれ以外のアセットをきちんと分けて配信したい方や、記事ごとにアセットを分けたい方向けに、Hexo にはアセットを管理する方法が組み込まれています。これは少し複雑ですが、アセットを管理するにはとても便利な方法で`_config.yml`内の`post_asset_folder`を true に設定すると有効化できます。

```yaml _config.yml
post_asset_folder: true
```

アセットフォルダ管理を有効化すると、`hexo new [layout] <title>`コマンドで新しい記事を作るたびに Hexo はフォルダを作成します。このアセットフォルダ名は記事の markdown ファイル名と同じになります。簡単にそしてより便利にするため、記事に関連する全てのアセットをフォルダに入れて頂くと、相対パスを使って参照することがでます。

## 相対パス参照のためのタグプラグイン

通常の markdown 構文を使った画像やその他のアセット参照では、アーカイブまたはインデックスページにおいて相対パスは誤った表示になる可能性があります。Hexo2 でこの問題に対応するためコミュニティによってプラグインが作成されました。しかし、Hexo3 のリリースに伴っていくつかの新しい[タグプラグイン](/docs/tag-plugins#Include-Assets)がコアに追加されました。これによって記事内でより簡単にアセットを参照することができます。

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

例えば、アセットフォルダを有効化した場合、画像ファイル`example.jpg`をアセットフォルダに格納して、一般的な markdown 構文である`![](example.jpg)`で相対パスを使って参照しても、インデックスページには表示**されません**。（しかし、記事では期待通り表示されます）

画像を正しく参照するには、markdown ではなくタグプラグイン構文を使用します：

```
{% asset_img example.jpg This is an example image %}
{% asset_img "spaced asset.jpg" "spaced title" %}
```

この方法で、画像は記事やインデックスページ、アーカイブページすべてで表示されます。

## markdown を使用した画像の埋め込み

[hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked) 3.1.0 では、タグプラグイン`asset_img`を使用しなくても markdown で画像を埋め込むことができます。

有効化の方法：

```yml _config.yml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

有効化すると、アセット画像はそれに対応した記事のパスに自動的に解決されます。例えば、"image.jpg"が"/2020/01/02/foo/image.jpg"に格納されていた場合、"/2020/01/02/foo/"記事のアセット画像と認識され、`![](image.jpg)` は `<img src="/2020/01/02/foo/image.jpg">`として描画されます。
