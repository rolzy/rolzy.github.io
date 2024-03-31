---
title:  "Vim入門③ - 縦の移動"
date:   2024-03-28 00:00:00 +1000
tags: Vim 日本語
read_time: false
comments: true
classes: wide
toc: true
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png
---

{% capture notice-text1 %}
この記事はVim入門シリーズの第3弾です。 初めての方は過去記事もどうぞ:
- 第1弾: [Vimの4つのモード](https://www.rolzy.net/2024/01/28/vim-nyuumon.html)
- 第2弾: [横方向の移動](https://www.rolzy.net/2024/01/28/vim-nyuumon.html)
{% endcapture %}

<div class="notice--info">
  <h4 class="no_toc">はじめに</h4>
  {{ notice-text1 | markdownify }}
</div>

今回はVim入門シリーズ第3弾、縦の移動について徹底解説していきます！

## おさらい
前々回の記事にて、**h, j, k, l** キーで移動できることについて軽ーく触れました。
jキーで下に一文字移動、kキーで上に一文字移動でしたね。

また、前回は移動する際に使えるコンビネーションもいくつか紹介しました。

今回も同じコンビネーションを使って上下に移動していきます！

ここまでの回を読めば、超スピードでカーソルを縦横無尽に移動できるようになります！
頑張っていきましょー！

## また回数指定
まず一つ目に紹介するテクニックが回数指定です。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/5j10kvanilla.gif" %}

そう、前回も紹介した、**移動コマンドの前に回数を指定する**アレです。

例えば、上に5行移動する場合は`5k`、下に7行移動する場合は`7j`と打ちます。

しかし、この回数指定のネックも前回紹介しました。そう、**目視で何行移動するか判断するのはムズカシイのです。**

でも、縦移動の場合のみ、強力な助っ人がいるんです。

### Line numbering で行数を表示する
前々回、コマンドモードを紹介しました。`:`の後にコマンドを書いて、Vimを動かすモードです。
ファイル保存するときに打つ`:wq`もコマンドモード使ってますね。

もちろん、コマンドモードの機能はそれだけでなく、Vimの設定もイジることができます。
`:set ○○`で、いろんな機能を付けたり消したりできちゃうんです。

今回紹介するのは`set number`および`set nu`。これを打つと、画面左端に行数を表示してくれるようになります。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/setnu.gif" %}

これがあれば、回数指定もちょっと楽になりますよね！今いる行と移動したい行で引き算すればいいわけd...

**<span style="font-size:2em;font-family:sans-serif;color:red;">遅い!遅すぎる!!!</span>**

行間を移動するたびにいちいち引き算してたら日が暮れてしまうので、ちょっと機能を拡張しましょう。

### Relative line numbering で相対的な行数を表示
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/setrnu.gif" %}
Vimにて`:set relativenumber`および`:set rnu`と打つと、左端の行数がちょっと変わります。
なんと、今いる行を起点に上下に行数を数えていってくれるんです！

これ、画面左を見れば行きたい行がここからどれぐらいか一目でわかるので、
`j`と`k`の移動には欠かせない設定です。回数指定がすごい捗ります。

横の移動では微妙だった回数指定ですが、縦移動の場合はRelative Line Numberingと合わせることで化けるんです！
希望の行にすいすい移動できるようになります。

## もっと大きい距離を移動したい
これで`j`と`k`が100倍使えるようになったわけですが、それだけでは対応しきれないケースがあります。

**行数って画面の表示範囲内に制限されちゃうんです**

一応、`1000k` とかでかい数字を指定して移動することはできますが、それでは確実性がありませんし、大きい数字をタイピングしてるとそれはそれで遅いです。

大きい距離を連打で移動できるコマンドがあると便利ですよね。

そこで紹介するのが`Ctrl + u`と`Ctrl + d`。`Ctrl + u`(upのu)は上に20行、`Ctrl + d`(downのd)は下に20行移動できます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/ctrlud.gif" %}

Ctrl押しっパにして u or d 連打すればファイルを上下に早く移動できます。

マウスに手を伸ばさずに画面をスクロールできちゃうわけですねー！

## ファイル内で単語を検索したい
続いて紹介する移動方法はほかのエディタでもよく使われるものです。皆さん、ブラウザやWordなどで `Ctrl + f` で単語検索するときありますよね？
もちろん、Vimでもできます。

`/` と打った後に、検索したい単語を打ってEnterです。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/wordsearch.gif" %}

検索すると、最初のヒットがハイライトされて表示されると思います。
この状態から、次のヒットに移動したい場合は`n`、前のヒットに戻りたい場合は`b`で戻れます。

ピンポイントで移動したい単語がある時に使います。これはどのエディタにもある、共通の便利機能ですね。

## おまけ

### ファイルの先頭と後尾への移動
Vimでは、ノーマルモードから`gg`でファイルの先頭（一行目）に移動し、`G`で最後尾に移動できます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/ggG.gif" %}

### 段落を移動する
最後に、前後の段落に移動する方法を紹介します。

`Shift + {` と `Shift + }` です。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-03-31-vim-nyuumon-3/para.gif" %}

`Shift + {`で前の段落に移動、`Shift + }` で後方の段落に移動できます。

レポートやコードなど、まとまった文章を書いているときは使える場面もあります。

しかし、前回の `w`および`b`の紹介でも話したのですが、段落の判定ってVimのさじ加減になっちゃうんですよね。100％自分の思い通りに動いてくれるわけではないので、確実性に欠けます。

個人的には `Ctrl+u` `Ctrl+b`と回数指定のコンボで事足りると思ってます。段落の移動はあまりしません。

## おわりに
以上で、Vimでの縦の移動についての紹介を終わりにしようと思います。
もちろん、ほかにも移動方法はいろいろあるのですが、ここで紹介したもので大体事足りると思ってます。

この第3パートまでVimの移動は一通り終了です。ここまで読めばVimのカーソルを自由に動かせることができるようになると思います。

しかし、カーソルを動かしてるだけでは意味がないので、次回からは文章の編集方法についてガッツリ紹介していこうとおもいます。　
