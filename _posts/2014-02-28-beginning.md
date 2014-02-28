---
layout: post
title: 会社で技術ブログがはじまった
date: 2014-02-28
category : ohno
tags : [GitHub, GitHub pages, jekyll]
---

## コトノハジマリ

### ことの始まり

会社で技術ブログを開始することになった。[nagane](https://github.com/nagane)氏発案により始まった。月間で一番いい記事を書いたスタッフに社長から*ご褒美*が出るとのことで、参加してみることにした。

### GitHub Pagesでやるらしい

[nagane](https://github.com/nagane)氏から事前に相談を受けていたのだが、[GitHub Pages](http://pages.github.com) + [jekyll](http://jekyllrb.com)を使うことに決まったらしい。jekyllはちょっと前にいじった事があるので、少しは勝手が効きそうだ。

### とは言うものの

ブログ開始はいいのだが、技術ブログと言うのがお題である。*ブログのタイトルは『welox tech blog』。実にストレートだ。*私は技術職ではないため、記事に出来るような知識がない。困ったのでネタを探し始める。

### その前に…

ネタ探しの前に一つ疑問が。ブログの投稿者管理ってどうするんだろ？と[『welox tech blog』](http://welox.github.io)を覗いてみる。jekyllにはcategory機能ってのがあるみたいで、これで代替出来そう。GitHubの練習をかねてIssue機能を使ってみる。[Issue](https://github.com/welox/welox.github.io/issues/3)を追加。さてネタ探し。

## ムチャブリ

### 記事作成依頼

ネタでも探すか。と思ったら、nagane氏から『ページ更新までの流れ』を記事にするように依頼が来た。Git/GitHubの練習もかねてブランチやプルリクを使ったフローにするとのこと。とりあえず書いてみる。

## ブログコウシンノナガレ

### 更新フロー
1. ([GitHub](https://github.com/welox/welox.github.io)で作業)GitHubアカウントの作成（最初だけ）
- [nagane](https://github.com/nagane)氏にアカウント名を伝える（最初だけ）
- ローカルにwelox/welox.github.ioのクローンを作成する（最初だけ）
- 更新用のブランチを作成する
- 新ブランチでyyyy-mm-dd-title.mdを作成する
- _postsディレクトリにyyyy-mm-dd-title.mdを配置する
- 変更をadd、commit、pushする
- (GitHubで作業)pushした内容をmasterブランチにPull Requestする
- (GitHubで作業)Pull RequestをMergeする
- (GitHubで作業)不要なブランチは削除する

### ターミナルでの操作方法

```
$ git config --global user.name hoge #名前を登録する（最初だけ）
$ git config --global user.email hoge@welox.jp #メールアドレスを登録する（最初だけ）
$ git clone git@github.com:welox/welox.github.io.git #クローンを作成する（最初だけ）
$ cd welox.github.io.git #ディレクトリ移動
$ git branch hoge #hogeブランチを作成する
$ git checkout hoge #hogeブランチに切り替え
（yyyy-mm-dd-title.mdを作成）
$ git add 2014-03-01-fuga.md #変更をaddする
$ git commit -m 'Create 2014-03-01-fuga.md' #変更をcommitする
$ git push origin hoge #変更をpushする
```

### 記事ファイル（yyyy-mm-dd-title.md）の記述方法

```
--- #このまま。
layout: post #このまま。よくわかってない。
title: 会社で技術ブログがはじまった #タイトル。
date: 2014-02-28 #日付。
category : ohno #名前。毎回同じに。
tags : [GitHub, GitHub pages, jekyll] #タグ。好きにつけて。
--- #このまま。

本文 #本文をここに。Markdown記法が使える。
```

### 参考サイト

- Git/GitHubは[ここ](http://blog.qnyp.com/2013/05/28/pull-request-for-github-beginners/)を参考にした。
- jekyllは[ここ](http://krakenbeal.blogspot.jp/2012/05/ruby-jekyll-jekyll-bootstrap.html)を参考にした。

### その他

- 内容に誤りがある可能性があります。自己責任で。
- 2回目以降はgit pullが必要かな？
- [GitHub Mac](http://mac.github.com)や[SourceTree](http://www.sourcetreeapp.com)を使うと楽。
