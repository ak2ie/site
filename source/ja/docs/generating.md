---
title: 生成
---

Hexo では、とても簡単に速く静的ファイルを生成できます。

```bash
$ hexo generate
```

{% youtube viEJQPVCoLU %}

### ファイル変更の監視

Hexo ではファイル変更を監視し、すぐにファイルを再生成できます。Hexo はファイルの SHA1 チェックサムを比較し、変更を検知した場合のみ出力します。

```bash
$ hexo generate --watch
```

### 生成後の公開

生成後に公開するためには、次のいずれかのコマンドを実行します。2 つに違いはありません。

```bash
$ hexo generate --deploy
$ hexo deploy --generate
```
