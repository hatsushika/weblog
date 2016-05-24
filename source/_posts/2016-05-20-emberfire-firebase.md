---
title: FireBase試し (EmberFire)
id: 76
categories:
  - emberjs
date: 2016-05-20 02:05:20
tags: emberjs
---

Google i/oでFirebaseが気になったので試しにどんなものかさわってみた
https://events.google.com/io2016/

## ■ 環境

node v4.4.4
npm v2.15.1
bower v1.7.9

ember v2.5.1
ember-cli v2.5.0
emberFire v1.6.6

### EmberFireのTutorialを参考に試してみる

https://www.firebase.com/docs/web/libraries/ember/

### Guide

https://www.firebase.com/docs/web/libraries/ember/guide.html

## ■ 準備

### FireBase ConsoleでApp作成

<img src="/weblog/img/p1.png" width="300" height="141">

## ■ 作成

### Ember App 作成

#### ember-cliを利用してAppを作成
```
$ ember new emberFire-study
```

### emberFireインストール

#### こちらもember-cliを使用してemberFireをインストール

```
$ ember install emberfire
```

インストールすると「bower.json」と「app/adapters/application.js」に
emberFireが追記されていることがわかる

### emberFire設定

* 「config/environment.js」内の先ほど作成したfirebaseのURLを設定する

```
firebase:'https://YOUR-FIREBASE-APP.firebaseio.com/'
```

### データ作成用にモデル作成

ember-cliでモデルを作成
```
$ ember generate model post title:string body:string timestamp:number
```

app/models/post.js
```javascript
export default DS.Model.extend({
  title: DS.attr('string'),
  body: DS.attr('string'),
  timestamp: DS.attr('number')
});
```

### データ作成用にテンプレート作成

```
$ ember generate template posts
```

### データ投入処理追加

*   template

```html
<h2>New Post</h2>
<ul class="post-publish">
  <li>
    {{input value=title placeholder="Title"}}
  </li>
  <li>
    {{textarea value=body placeholder="Body"}}
  </li>
  <li>
    <button {{action "publishPost"}}>Publish</button>
  </li>
</ul>
```

* controller

```
$ ember generate controller posts
```
```javascript
import Ember from 'ember';

// app/controllers/posts.js
export default Ember.Controller.extend({
  sortProperties: ['timestamp'],
  sortAscending: false, // sorts post by timestamp
  actions: {
    publishPost: function() {
      var newPost = this.store.createRecord('post', {
        title: this.get('title'),
        body: this.get('body'),
        timestamp: new Date().getTime()
      });
      newPost.save();
    }
  }
});
```

### サーバを立ち上げ動作確認

```
$ ember s
```

http://localhost:4200/

<img src="/weblog/img/p2.png" width="300" height="186">

http://localhost:4200/posts

<img src="/weblog/img/p3.png" width="300" height="141">

「Publis」ボタンを押してblogを投稿

### FireBase Console画面にて確認

<img src="/weblog/img/p4.png" width="300" height="124">

無事登録されていることを確認

### データ一覧を参照する処理を追記

* route

```
$ ember generate route posts
```

途中でTemplesを上書きするか聞いてくるので取り敢えず「No」！
```javascript
export default Ember.Route.extend({
  model: function() {
    return this.store.findAll('post');
  }
});
```

先ほどのtemplesに下記を追記
```html
<section>
{{#each model as |post|}}
  <div>{{post.title}}</div>
  <div>{{post.body}}</div>
{{/each}}
</section>
```

### サーバを立ち上げ動作確認

```
$ ember s
```
http://localhost:4200/posts

<img src="/weblog/img/p1.png" width="245" height="300">

上記の通り登録したものが表示されればOK。
他にもコメントなどのリレーションのコードもあるが割愛ｗ

## GitHub

[github](https://github.com/tetuo41/emberFire-study)
