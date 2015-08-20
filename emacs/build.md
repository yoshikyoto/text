---
layout: default
title: Emacsをソースからビルドする
---


# Emacsをソースからビルドする

## 背景

Emacs23とEmacs24では結構違う部分も多く、Emacs24では動くのですが、Emacs23では動かないプラグインなんかも存在します。
いっぽうで、apt-getやyumで入れたりするとEmacs23が入ってしまい、困ることがあります。
そこで、Emacsをソースからビルドします。

なお、WindowsでEmacsを使おうとしている場合、ここの情報はあまり参考になりません。
また別にWindows向けのインストールページを作成予定なのでお待ちください。


## 最初に

Emacsをビルドするために必要な gcc, make などをインストールします。

### Cent OS の場合

```
sudo yum -y install gcc make ncurses-devel 
```

### ubuntuの場合

ubuntuの場合、gcc, make, ncurses-dev が入っていることを確認してください

```
$ sudo apt-get install gcc make ncurses-dev
```

もしこれで、下の方に書いてあるビルドができない場合、裏ワザ的に以下のコマンドを使う方法があります。

```
$ sudo apt-get build-dep emacs24
```

もっとスマートな解決法を探しておりますので、少々お待ちください。


### Macの場合

Macはdeveloper toolsを入れておけば問題ないような気がします。
ただし未確認ですので、また確認しましたら正確なものを記述します。


## ビルドしたいバージョンのemacsを探す

http://ftp.jaist.ac.jp/pub/GNU/emacs/ から、ビルドしたいEmacsのバージョンのtar.gzを探します。今回は24.5だとします。
magitという、Emacs上で動くGitのクライアントが、Emacs 24.4 以降でないと動作しないため、
これより新しいものを入れることをオススメします。


## ダウンロードしてビルドする

emacs 24.5 のURLは [http://ftp.jaist.ac.jp/pub/GNU/emacs/emacs-24.5.tar.gz]  なので、
これをダウンロードして解凍してビルドします。

```
$ wget http://ftp.jaist.ac.jp/pub/GNU/emacs/emacs-24.5.tar.gz 
$ tar xvf emacs-24.5.tar.gz 
$ cd emacs-24.5 
$ ./configure 
$ sudo make
$ sudo make install
```

`./configure` あたりで失敗する場合は、ビルドに依存するパッケージが正しくない可能性があります。
何か問題がありましたら、このページのGitHubのIssueなどで報告してください。


## path を通す

古いEmacsが存在していたりすると、pathが通らなかったりするので、その場合はpathを通す必要があります。

試しにEmacsのバージョンを調べてみてください。

```bash
$ emacs --version
GNU Emacs 24.5.1
...
```

自分のダウンロードしたEmacsのバージョンと同じ場合は問題ありません。
違う場合は以下の用にpathを変更してやります。

```
$ emacs --version
GNU Emacs 23.1
...

$ which emacs
/usr/bin/emacs
sudo rm /usr/bin/emacs

$ sudo ln -s /usr/local/bin/emacs-24.5 /usr/bin/emacs

$ emacs --version
GNU Emacs 24.5.1
...
```


## おわりに

とりあえずEmacsをビルドする方法を書きました。
次は、Emacsの操作や、カスタマイズの方法あたりについて書こうと思います。
