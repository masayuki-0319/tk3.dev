---
title: rubyinstaller で Ruby をインストールする (Windows)
date: 2011-03-03T00:00:00+09:00
slug: 26ce7277c5e2595d3909842cb881b0ced749a63e
---

## 1. rugyinstaller をダウンロードする
rubyinstaller-1.9.2-p180.exe をダウンロードする。


## 2. インストーラーを実行する
[Installation Destination and Optional Tasks] のとき [Add Ruby executables to your PATH] をチェックすると、
ユーザーの環境変数 PATH に自動で実行ファイルへのパスを追加してくれる。


## 3. インストールを確認する
コマンドプロンプトを起動し、ruby -v を実行する。

```
C:\Users\foo>ruby -v
ruby 1.9.2p180 (2011-02-18) [i386-mingw32]

C:\Users\foo>gem -v
1.5.2

```


## 4. 続いて DevelopKit をインストールする

### 4.1 DevKit をダウンロードする
DevKit-tdm-32-4.5.1-20101214-1400-sfx.exe をダウンロードする

### 4.2 ダウンロードしたファイルを展開する
ダウンロードしたファイルを実行し、ファイルを展開する。
展開したファイルをインストールしたいパスに移動させる。
インストール後も使用されるので、注意。

### 4.3 インストールする

```
C:\Users\foo\opt\Ruby192\devkit-4.5.1>ruby dk.rb init
[INFO] found RubyInstaller v1.9.2 at C:/Users/foo/opt/Ruby192

Initialization complete! Please review and modify the auto-generated
'config.yml' file to ensure it contains the root directories to all
of the installed Rubies you want enhanced by the DevKit.

C:\Users\foo\opt\Ruby192\devkit-4.5.1>ruby dk.rb install
[INFO] Updating convenience notice gem override for 'C:/Users/foo/opt/Ruby192'
[INFO] Installing 'C:/Users/foo/opt/Ruby192/lib/ruby/site_ruby/devkit.rb'

```
