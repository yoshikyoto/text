---
layout: default
title: git stash まわりの操作
---

# git stash まわりの操作

## とりあえず何がstashしてあるのか確認する

```
$ git stash list
stash@{0}: WIP on <branch>: HogeHoge
stash@{1}: WIP on ...

$ git diff HEAD..stash@{0}
# これでdiffが見られる
```


## stash@{0} と今の状態との差分を見てみる

```
$ git stash show
 .gitignore                                  |  3 ++-
...
```


## checkoutして適切な方を選択

```
$ git checkout stash@{0} .gitignore
```

* stash show の結果は変わっていないが、手元のファイルは変更されている


## stash listを消す

```
$ git stash drop stash@{0}
```

## ここから生まれたgitconfig

```
[alias]
 diff-stash = "!f() { git diff HEAD..stash@{$1}; };f"
 stash-list = stash list
 stash-pop = "!f() { if [ $# -eq 0 ]; then git stash pop; else git stash pop stash@{$1}; fi; };f"
```

使い方

```
$ git stash-list
# stash一覧を見る

$ git diff-stash 1
# stash@{1} と HEAD の diff を見る

$ git stash-pop 1
# stash@{1} を pop する
```

まだまだ使いやすくしたい。
