---
title: Linuxでログイン出来ないユーザをログイン出来るように変更する
id: 11
categories:
  - Linux
date: 2013-07-03 12:19:03
tags:
---

[bash]
$ su testuser
This account is currently not available.
[/bash]
↑こんなヤツが出る場合

testuserには「/sbin/nologin」が設定されている
なので「/bin/bash」に変更して上げる
[bash]
$ usermod -s /bin/bash testuser
[/bash]
</br>
参考URL：
http://server-setting.info/centos/login_user.html