---
title: Documentation
---

Hexo ドキュメントへようこそ。Hexo をお使いの上で問題が発生したら、[トラブルシューティングガイド](troubleshooting.html)をご覧頂くか、[GitHub](https://github.com/hexojs/hexo/issues)に issue を投げるか、[Google Group](https://groups.google.com/group/hexo)に投稿してください。

## Hexo とは何か？

Hexo は速くて、シンプルで、パワフルなブログフレームワークです。[Markdown](http://daringfireball.net/projects/markdown/) (または、その他のマークアップ言語)で記事を書いたり、魅力的なテーマで静的なファイルをすぐに生成できます。

## インストール

Hexo はすぐにセットアップできます。問題を解決できないようでしたら、[GitHub に issue を投稿](https://github.com/hexojs/hexo/issues)してください。

{% youtube ARted4RniaU %}

### 動作環境

Hexo のインストールはとても簡単です。あらかじめ次の環境が必要です。

- [Node.js](http://nodejs.org/) (Node.js 10.13 以上が必須, 12.0 以上を推奨)
- [Git](http://git-scm.com/)

すでにインストール済でしたら、[Hexo インストール](#Install-Hexo)に進んでください。

まだインストールしていない場合は、次の手順に従って動作環境をセットアップしてください。

### Git のインストール

- Windows: [git](https://git-scm.com/download/win)からダウンロードしてインストール
- Mac: [Homebrew](https://brew.sh/) または [MacPorts](http://www.macports.org/)、[installer](http://sourceforge.net/projects/git-osx-installer/)からインストール
- Linux (Ubuntu, Debian): `sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS): `sudo yum install git-core`

{% note warn Macユーザーの方へ %}
コンパイル時に問題が発生するかもしれません。はじめに、App Store から Xcode をインストールしてください。インストール後、Xcode を開いて**Preferences -> Download -> Command Line Tools -> Install**から command line tools をインストールしてください。
{% endnote %}

### Node.js のインストール

Node.js では多くの環境に対応した[公式インストーラー](https://nodejs.org/en/download/)が提供されています。

他のインストール方法:

- Windows: [nvs](https://github.com/jasongin/nvs/) (推奨) または [nvm](https://github.com/nvm-sh/nvm)を使用。
- Mac: [Homebrew](https://brew.sh/) または [MacPorts](http://www.macports.org/)を使用。
- Linux (DEB/RPM-based): [NodeSource](https://github.com/nodesource/distributions)を使用。
- Others: それぞれのパッケージマネージャからインストール。Node.js の[ガイド](https://nodejs.org/en/download/package-manager/)参照。

Mac と Linux では、権限による問題を回避するために nvs を推奨します。

{% note info Windows %}
公式インストーラーを使用する場合、「Add to PATH」（デフォルト ON）を ON にしてください。
{% endnote %}

{% note warn Mac / Linux %}
Hexo のインストール中に`EACCES`権限エラーが発生した場合、npmjs の[回避策](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)に従ってください。root/sudo での上書きは推奨されません。
{% endnote %}

{% note info Linux %}
Snap を使用して Node.js をインストールする場合、[初期化](/docs/commands#init)する際、フォルダ内において手動で `npm install` を実行する必要があります。
{% endnote %}

### Hexo のインストール

動作環境のソフトウェアのインストールが完了したら、npm で Hexo をインストールします。

```bash
$ npm install -g hexo-cli
```

### 上級者向けインストール方法

上級者の方は`hexo`パッケージをインストールして使用することもできます。

```bash
$ npm install hexo
```

インストールが完了したら、2 つの方法で Hexo を実行できます。

1. `npx hexo <command>`
2. Linux の場合、`node_modules/` フォルダの相対パスを設定します

```bash
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

`hexo <command>`で Hexo を使用できます。

### 最低限必要な Node.js バージョン

古いバージョンの Node.js を使用している場合、Hexo の過去のバージョンをインストールしたくなるかもしれません。

過去のバージョンの Hexo でのバグは修正されないことに注意してください。

可能な限り、Hexo の[最新バージョン](https://www.npmjs.com/package/hexo?activeTab=versions) と Node.js の[推奨バージョン](#Requirements)を使用することを強く推奨します。

| Hexo バージョン | 最低限必要な Node.js バージョン |
| --------------- | ------------------------------- |
| 5.0+            | 10.13.0                         |
| 4.1 - 4.2       | 8.10                            |
| 4.0             | 8.6                             |
| 3.3 - 3.9       | 6.9                             |
| 3.2 - 3.3       | 0.12                            |
| 3.0 - 3.1       | 0.10 or iojs                    |
| 0.0.1 - 2.8     | 0.10                            |
