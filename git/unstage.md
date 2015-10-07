---
layout: default
title: addしたファイルをaddする前に戻したい
---

# addしたファイルをaddする前に戻したい

## gitでaddしたファイルをaddする前に戻したい時のコマンド

```
$ git reset HEAD <ファイル名>
```

## ここから生まれたgitconfig

```
[alias]
  stage = add
  unstage = reset HEAD
```
