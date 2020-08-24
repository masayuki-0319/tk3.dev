---
title: CentOS5.4 に Go をインストールする
date: 2010-01-01T23:31:20+09:00
slug: 79d653f3f418e57ef54ac0fda306f9e13fcc0c19
---

現在の最新版にするために再度 Go をインストールしてみた。

** 0. 事前準備
ソースコードを取得するために mercurial を事前にインストールしておく。

```
# yum install python-setuptools
# yum install python-devel
# easy_install mercurial
```

** 1. 必要な環境変数を設定する。
.bashrc に環境変数を設定し、設定を反映させる。

*** .bashrc
```
# for Google Go
export GOROOT=$HOME/opt/go
export GOBIN=$GOROOT/bin
export GOARCH=386
export GOOS=linux
export PATH=$PATH:$GOBIN
```

設定を反映する。
```
$ . ~/.bashrc
```

** 2. ソースコードを取得する

```
$ hg clone -r release https://go.googlecode.com/hg/ $GOROOT
requesting all changes
adding changesets
adding manifests
adding file changes
added 4477 changesets with 18997 changes to 3098 files
updating working directory
1793 files updated, 0 files merged, 0 files removed, 0 files unresolved
```

** 2. コンパイルする
実行モジュールがインストールされるディレクトリを作成する。
このディレクトリを作成していないと後にエラーになる。

```
$ mkdir $GOBIN
```

ソースコードを落としたディレクトリに移動し、コンパイルする。
```
$ cd $GOROOT/src
$ ./all.bash
```

** 3. 動作確認

```
$ cat hello.go
package main

import "fmt"

func main() {
    fmt.Printf("hello, world\n")
}

$ 8g hello.go
$ 8l hello.8
$ ./8.out
hello, world
```
