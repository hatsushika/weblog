---
title: Linuxでログイン出来ないユーザをログイン出来るように変更する
id: 11
categories:
  - Memo
date: 2013-07-03 12:19:03
tags: 
  - linux
---

```
$ su testuser
This account is currently not available.
```
↑こんなヤツが出る場合

testuserには「/sbin/nologin」が設定されている
なので「/bin/bash」に変更して上げる

`$ usermod -s /bin/bash testuser`

</br>

Thanks for the link.
http://server-setting.info/centos/login_user.html
