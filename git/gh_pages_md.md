---
layout: default
title: Markdownで書かれたページをGitHub Pagesで公開する
---

# Markdownで書かれたページをGitHub Pagesで公開する

GitHub Pagesを使えば、MarkdownをHTMLに変換して公開することができます。
設定さえすれば、MarkdownをGitHubのリポジトリにPushしたことをトリガーにして、
勝手にHTMLに変換してくれた上で公開までしてくれます。
このページもその方法で公開されています。
GitHub上のエディターで編集すれば手元に何も要りませんし、非常に便利です。


## GitHub Pages の設定

GitHub Pagesとは、リポジトリにHTMLなどをPushすると、それをWebページとして公開してくれるサービスのことです。
ここでは以下の2種類のGitHub Pagesについて説明します。
https://help.github.com/categories/github-pages-basics/ にヘルプがあります。

* ユーザーのページ
* リポジトリごとのページ

### ユーザーのページ

`<username>.github.io` というリポジトリを作成すると、ユーザーのページが作成できます。
これは、ユーザーが自分のページを公開するために使います。
以下の手順で公開します。

1. このリポジトリの `master` に `index.html` などをPushします。
2. リポジトリのSettingsから、Launch automatic page generator というボタンを押します。
3. `Your site is published at http://<username>.github.io.` と表示され、このURLでページが公開されます。


### リポジトリのページ

これは、リポジトリで管理しているプロジェクトに関するページを公開するために使います。

1. リポジトリに、`gh-pages` というブランチを作ります。
2. そのブランチに、 `index.html` などをPushします。
3. 以下、ユーザーのページと同様です。

ブランチが `gh-pages` になるだけで、他はユーザーのページと変わりません。
masterはプロジェクトのコードのmasterで、gh-pagesは公開するページのマスターということになります。


## Markdownで書かれたページを公開する

jekyllという、MarkdownをHTMLに変換してくれるツールがあり、
GitHub Pagesはこれを使ってMarkdownをHTMLに変換しているようです。
というわけで、jekyllの設定をします。
公式のヘルプは http://www.comico.jp/special/index.nhn?docno=3 にありますが、
ハマった点なども含めて順番に書いていきます。


### 必要なファイルとディレクトリ構成

実際に僕のリポジトリ(https://github.com/yoshikyoto/text)を見るのが早いのかもしれませんが、
必要なファイルはこんな感じです。

* _config.yml
* _layouts
  * defaut.html
* index.md

ルートに、jekyllのびルドの設定を書いた `_cinfig.yml` 、 `_layouts` ディレクトリ下に `適当な名前.html` とかいたファイル、そしてマークダウンのファイルです。

### Config

`_config.yml` はこんな感じの内容になっています。

```
markdown: redcarpet
redcarpet:
  extensions: ["no_intra_emphasis", "fenced_code_blocks", "autolink", "strikethrough", "superscript"]
```

`markdown: redcarpet` は、Markdownのレンダリングにredcarpetというエンジンを使いますよ的な意味です。
これを指定しないと一部ちゃんと変換されない箇所がありました。

`extensions` は、以下のものが指定できるようです。

* autolink
* fenced_code_blocks
* lax_spacing
* no_intra_emphasis
* space_after_headers
* strikethrough
* superscript
* tables

詳しくは https://github.com/vmg/redcarpet のREADMEを呼んで欲しいのですが、きれいにレンダリングしてくれるためのあれこれです。
例えば、autolinkはURLを書くと自動でリンクに変換してくれる拡張です。

これらの設定に加え、特に指定がなければ、GitHub側で `highlighter: pygments` が指定されます。
これは、コードのシンタックスハイライトをしてくれるものです。

さらに、`safe: true` や `lsi: false` は設定しても上書きされるらしいですが、
セキュリティ上の問題なのであまり気にしなくていいでしょう。


### _layouts

defaultという名前はなんでもいいです。
例えば、 `_layouts/defaut.html` を以下のようにします。

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8'>
    <title>｛｛ page.title ｝｝ - @yoshiki_utakata</title>
  </head>

  <body>
    ｛｛ content ｝｝
  </body>
</html>
```

`｛｛ content ｝｝` の部分に、MarkdownをHTMLに変換したものが入ります。（`｛`, `｝`は半角にしてください。）
`｛｛ page.title ｝｝` の部分については後に説明します。


### Markdownファイル

Markdownファイルを以下のように書きます。

```
---
layout: default
title: トップページ
---

# トップページです

* hoge
* huga
```

`layout` で `default` を指定しているので、 `_layouts/default.html` というレイアウトを適用します。
`title` の中身が `page.title` の部分に入ります。


## 公開方法

以上のものを用意し、あとは最初に書いた、GitHub Pages の公開手順と同じ手順を踏むことで、ページが公開できます。

cssなども適用できるので、 https://github.com/yoshikyoto/text/ などを参考にしてください。


## ハマった点

レンダリングに失敗すると、Build Error メールが飛んできます。例えばコードブロックで、

```
｀｀｀bash

｀｀｀
```

のような記述をすることがあります。これをGitHubはよしなに解決してくれるのですが、
redcarpetの場合、「bashなんていうものはねぇ！」と言って起こってきます。
エラー通知はメールが来るのですが、どこでエラーになっているのかはメールでは教えてくれません。
このエラーを確認するためには、手元でjekyllをインストールして動かすしかないのですが、
バージョンやビルドのオプションが異なり、手元ではエラーが出ない場合があります。
