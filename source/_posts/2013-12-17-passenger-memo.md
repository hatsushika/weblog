---
title: Passenger Memo
id: 52
categories:
  - Memo
date: 2013-12-17 11:04:55
tags: 
  - linux
---

# 必要なモノをインストール
```
$ yum install httpd httpd-devel apr-devel apr-util-devel curl-devel
```

# Passengerをインストール
```
$ gem install passenger
```

# apache moduleインストール
```
$ passenger-install-apache2-module
```

# 設定ファイル追加
```
LoadModule passenger_module ～/mod_passenger.so
PassengerRoot ～/passenger-x.y.z
PassengerDefaultRuby ～/ruby
```

# httpd.conf 変更追加
```
$ vi /etc/httpd/conf.d/passenger.conf
```

Thanks for the link.
http://babiy3104.hateblo.jp/entry/2013/08/30/193034
http://morizyun.github.io/blog/passenger-install-apache-ruby-rails/
http://petitviolet.hatenablog.com/entry/20130804/1375604128
