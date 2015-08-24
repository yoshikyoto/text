---
layout: default
title: ソースから最新版のgitを入れる
---

# yumで入れたgitのバージョンが低すぎるのでupdateする

`git stash -u` とかが動かないので、なんでかなと思ったら、gitのバージョンが古いからだった。

とりあえずgitのバージョンを調べて、適当にリネームしてgitコマンドが効かないようにする。

```
$ git --version
git version 1.7.1

$ sudo mv /usr/local/bin/git /usr/local/bin/git-1.7.1

$ git
no such command: git
```

まず、 https://www.kernel.org/pub/software/scm/git/ から欲しいgitのバージョンのtar.gzを探す。
今回は執筆時点での最新版である `2.5.0.tar.gz` を入れてみることにする。

```
$ sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-ExtUtils-MakeMaker

$ wget https://www.kernel.org/pub/software/scm/git/git-2.5.0.tar.gz
$ tar zxf git-2.5.0.tar.gz
$ cd git-2.5.0
$ make
$ make install

$ git --version
git version 2.5.0

$ which git
~/bin/git
```

ファッ？！そのままだと `ホームディレクトリ/bin/git` にディレクトリが作成されてしまうようだ。
というわけでやりなおす。

```
$ rm -r ~/bin

$ make prefix=/usr/local all
$ sudo make prefix=/usr/local install

$ git --version
git version 2.5.0

$ which git
/usr/local/bin/git
```

