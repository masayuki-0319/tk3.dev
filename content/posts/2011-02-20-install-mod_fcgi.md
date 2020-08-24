---
title: mod_fcgid のインストール
date: 2011-02-20T00:00:00+09:00
slug: 570da1e2376afb3d163c30b65f80c0191a9eec8d
---

** 環境
- CentOS release 5.5 (Final)
- httpd-2.2.3-43
- httpd-devel-2.2.3-43


** 1. mod_fcgid のソースコードをダウンロードする
http://httpd.apache.org/mod_fcgid/ から mod_fcgid のソースコードを取得する


** 2. ビルド && インストール
ソースコードを展開し、コンパイルする。
コンパイルに成功したら、インストールを行う。

```
# tar zxf mod_fcgid-2.3.6.tar.gz
# cd mod_fcgid-2.3.6
# ./configure.apxs
# make
# make install
```


** 3. mod_fcgid の設定を行う
apache の conf.d に mod_fcgid の設定ファイルを置く

```
# cat /etc/httpd/conf.d/fcgid.conf
<IfModule mod_fcgid.c>
    AddHandler fcgid-script .fcgi
    SocketPath /tmp/fcgid_sock/
    IPCConnectTimeout 20
    MaxProcessCount 8
    DefaultMaxClassProcessCount 2
    TerminationScore 10
    SpawnScore 80
    IdleTimeout 300
</IfModule>
```


** 参考
- [http://www.movabletype.jp/documentation/developer/server/fastcgi.html:title=FastCGIのインストールと設定]
