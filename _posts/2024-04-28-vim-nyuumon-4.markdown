---
title:  "Vim入門④ - 文章の編集"
date:   2024-04-28 00:00:00 +1000
tags: Vim 日本語
read_time: false
comments: true
classes: wide
toc: true
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png
---

{% capture notice-text1 %}
この記事はVim入門シリーズの第4弾です。 初めての方は過去記事もどうぞ:
- 第1弾: [Vimの4つのモード](https://www.rolzy.net/2024/01/28/vim-nyuumon.html)
- 第2弾: [横方向の移動](https://www.rolzy.net/2024/02/28/vim-nyuumon-2.html)
- 第3弾: [縦方向の移動](https://www.rolzy.net/2024/03/28/vim-nyuumon-3.html)
{% endcapture %}

<div class="notice--info">
  <h4 class="no_toc">はじめに</h4>
  {{ notice-text1 | markdownify }}
</div>

今回はVim入門シリーズ第4弾、文章の編集です。

皆さん、過去三回の記事でVim内の移動はマスターされたかと思います!

また、移動だけでなく、より根源にあるVimの4つのモードの使い方も少しずつ身についてきたかと思います。

今回からは移動へのフォーカスを外し、文章の編集について詳しく見ていきます。

## そもそも編集って？
**「文章の編集」**と一言にいっても、その定義は広いです。

「文章の編集」と聞いてまず思いつくのが**「文章の入力」**かと思います。

従来のワードプロセッサーやIDEでは、この**「文章の入力」**がデフォルトです。例えば、Microsoft Wordを開いて文字を入力すると、文章の入力が行われます。

でも、Vimはそうではありません。**「文章の編集」**(ノーマルモード)がデフォルトなんです。
Vim初心者がつまづく一番の原因はここだと思います。

「文章の編集」は、単語を入れ替えたり、文章を動かしたり、コピペしたり、文章を削除したり。編集作業全般を指します。

Vimは、これらの編集作業全般ができるノーマルモードがデフォルトなんです。
これだけ多くの作業を**キーボードだけ**で出来るようにVimは設計されているのです。

覚えるコマンドは多いですが、以前紹介した移動コマンドと組み合わせれば覚えやすいと思います。

今回はノーマルモードやビジュアルモードを使った文章の編集を紹介します。

# コピー
`y`キーを押すと選択範囲をコピーできます。
コピーする時はコピーしたい文の範囲も併せて指名します。

例えば、第二回で紹介した横移動コマンドを使って、
- `yw` -> カーソル上の1単語をコピー
- `y5w` -> カーソルから先の5単語までをコピー
- `y$` -> カーソルから行末までコピー
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/yhorizontal.gif" %}

第三回で紹介した縦移動コマンドなら
- `y2j` -> カーソルから下2行までをコピー
- `y{` -> カーソル内の文節をコピー
- `yG` -> カーソルからファイルの終わりまでコピー
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/yvertical.gif" %}

…と、移動コマンドと組み合わせることで広範囲の編集が簡単になります。

ちなみにペーストは`p`でできます。ペーストは回数指定ができるので、`10p`と打てば同じ文章を10回ペーストしてくれます。

## テキストオブジェクトについて
**もしこの記事から一つ持ち帰るとすれば、マジでこれを覚えておいてもらいたいです。**

上記コマンドを試してみた方、`yw`や`y{`に違和感を覚えませんでしたか？

実はこのコマンド、**カーソルが対象の途中にある場合、カーソルから対象の終わりまでしかコピーしてくれません。**

単語や文節そのものをコピーしてくれないんです。

もし、カーソルの位置に関係なく単語や文節を全部コピーしたい場合、テキストオブジェクトを有効利用しましょう！

使い方は簡単です。
- `yiw`でカーソル内の単語をコピー
- `yaw`でカーソル内の単語+周りのスペースをコピー

…といった感じで、コマンドの間に`i`または`a`を入れることで使えます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/textobjects.gif" %}

コピーできる単位は`w`(単語),`(`(括弧),`"`(引用符),`{`(文節)などなど…

これを使うと編集コマンドの制度が爆上がりするので、使わない手はないです。
ぜひ試してみてください!

# 文の変更
`c`を押すと選択範囲を変更できます。
選択範囲にある文章が削除され、即座にインサートモードに切り替わります。

`y`と同じで、移動コマンドを使って選択範囲を指定します。
- `c0` -> カーソルから行頭まで変更
- `c2k` -> カーソルから上2行までを変更
- `ci(`でカーソルの括弧内の文章を変更
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/change.gif" %}

`c`で削除された元の文章はクリップボードにコピーされるので、`p`でペーストして復元できます。
{: .notice--info}

# 文の削除
`c`を押すと選択範囲を削除できます。

`y`および`c`と同じで、移動コマンドを使って選択範囲を指定します。
- `d4b` -> カーソルから前の四単語まで削除
- `dgg` -> カーソルからファイルの先頭まで削除
- `da"`でカーソルの引用符をまとめて削除
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/delete.gif" %}

# その他の編集コマンド
## 一文字編集コマンド
一文字だけ編集したいときは、文章範囲を指定するのもメンドクサイので下記コマンドを使いましょう。
- s (一文字変更)
- x (一文字削除)

## 大文字小文字
`~`で文字の大文字小文字を入れ替えられます。
範囲選択できるので、単語やカッコ内の文章の入れ替えもできます。

## 単語の検索と置き換え
第一回: Vimの4つのモードで紹介した**コマンドモード**を使って、単語の検索と置換ができます。
具体的には、ノーマルモード中に`:s`と入力することでコマンドモードに移行し`sed`と同じことができるようになります。

- `:s/before/after` -> カーソルがある行の一番初めに出てくる`before`を`after`に置き換え
- `:s/before/after/g` -> カーソルがある行に出てくる全ての`before`を`after`に置き換え
- `:1,5s/before/after/g` -> ファイルの1行目から5行目のすべての`before`を`after`に置き換え
- `:%s/before/after` -> 全行の一番初めに出てくる`before`を`after`に置き換え
- `:%s/before/after/g` -> ファイル内すべての`before`を`after`に置き換え
- `:%s/before/after/gc` -> `c`(checkのc)を入れると、置き換える前に確認ができます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-04-30-vim-nyuumon-4/sed.gif" %}

ちなみに、ビジュアルモードで範囲を指定してから`:s`と入力すると選択範囲で`sed`できます。

# おわりに
今回は、Vimを使った文章の編集コマンドをいくつか紹介しました。
特に`c` `y` `d`はVimの基本といってもいいコマンドで、よく使われます。

前回の移動コマンドと合わせて、より早いVimライフをエンジョイしましょう！
