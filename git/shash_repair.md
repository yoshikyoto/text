---
layout: default
title: stashした状態で編集とかしてよく分からなくなった場合の対処（ざっくり版）
---

# stash した状態で編集とかしてよく分からなくなった場合の対処（ざっくり版）

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
$git checkout stash@{0} .gitignore
```

* stash show の結果は変わっていないが、手元のファイルは変更されている
