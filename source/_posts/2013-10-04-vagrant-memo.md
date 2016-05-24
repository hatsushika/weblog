---
title: vagrant Memo
id: 46
categories:
  - memo
date: 2013-10-04 19:37:12
tags: memo
---

# 64bitだったver
`$ vagrant box add centos64_64 http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130427.box`

`$ init centos64_64`

# 32bitver
`$ vagrant box add centos64_32 http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-i386-v20130427.box`

# Vargrant認識 Vargrantファイル作成
`$ vagrant init centos64_32`

# 起動
`$ vagrant up`

# 仮想サーバー接続
`$ vagrant ssh`

# 停止
`$ vagrant halt`

# 削除
`$ vagrant destroy`

Thanks for the link.
http://k-holy.hatenablog.com/entry/2013/08/30/192243
