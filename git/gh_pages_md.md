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

