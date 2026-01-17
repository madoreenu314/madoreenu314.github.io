---
layout: post
title: Electronでデスクトップタイマー作ってみた
date: 2026-01-13 19:00 +0900
categories: computer coding
tag: JavaScript
image: /assets/pics/pomodoro.png
---

最近インスタでよく見かける[@nashallery](https://www.instagram.com/nashallery/)さんに触発され、彼女のチュートリアルビデオを見ながらElectronを使って簡易なポモドーロタイマーのデスクトップアプリを作ってみました。

<iframe src="https://www.youtube.com/embed/btxGSJ3Dh8E?si=W5rNpGDGsddSzfly" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

今まで深く考えずとりあえずmacデフォルトのターミナルを使っていましたが、VSCode内のを使えばわざわざ`cd`しなくていいんですね。。オートコレクションもあるみたいでとても便利だということに今更気づきました。

## Electronって？
Electronを使うと、web気分（JavaScriptとHTML&CSS）でデスクトップアプリが作れます。~~ググるとオワコンと出てきます。~~

```bash
npm install electron --save-dev
```

## 書けたの？

チュートリアルでとりあえずコピペするよう勧められたコード以外は書きました。結局そのコピペ部分も後々ウィンドウを小さくしたくなってちょいちょい手を加えました。

<iframe src="https://www.youtube.com/embed/_9QQf-RpPlM?si=p1cK4FfJhzGeuSnf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

JSでタイマーを作る方法が残念ながらほぼわからなかったので大枠はこの動画を参考にしました。しかしこの動画のタイマーではボタンが<kbd>START</kbd><kbd>STOP</kbd><kbd>RESET</kbd>の3つのみであり、作業用の25分しか測れなかったので、<kbd>WORK</kbd><kbd>BREAK</kbd><kbd>CLEAR</kbd>の3機能に自分なりに作りかえました。はじめWORK, REST, RESETの3単語を考え、なんか似ててダメだなとChatGPTに相談したら案をくれました。なんのために英語を学んできているのか。。

CSSは結構忘れていて勘で書きました。

## できたの？

とりあえず形になりました。自分専用のアプリを作ってみたかったのでできて嬉しいです！見た目も可愛いフォントを見つけたのでそこそこいい感じになりました。

<a href="https://github.com/madoreenu314/pomodoro"><img src="https://gh-card.dev/repos/madoreenu314/pomodoro.svg" width="440"></a>

## アプリとして使う際の備忘録

```bash
npm install --save-dev electron-reload
```

```js
if (!app.isPackaged) {
  require("electron-reload")(__dirname);
}
```
{: file="main.js" }
これを入れると、開発中は一度`npm start`で起動しておけば、ファイル変更を検知して自動で再起動/再読み込みしてくれるので、手動で起動し直す手間が減って便利です。


```bash
rm -rf dist
npm run build
open dist
```

これでdist直下にビルドされ、生成された`.dmg`から`.app`をApplicationsに入れれば、普通のアプリとして使えるようになります。

icnsファイルでアイコン画像を設定するとアプリアイコンが作れます。何もしないとElectronデフォルトの画像になります。公式アプリたちに並んで一丁前にアイコンが置かれるとおもしろいです。

![png](/assets/pics/pomodoroicon.png)
