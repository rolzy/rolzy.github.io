---
title:  "Vim入門② - 横の移動"
date:   2024-02-28 00:00:00 +1000
tags: Vim 日本語
read_time: false
comments: true
classes: wide
toc: true
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png
---

# はじめに
この記事はVim入門シリーズの第2弾です。 第1弾は[コチラ](https://www.rolzy.net/2024/01/28/vim-nyuumon.html)
{: .notice--info}

今回はVim入門シリーズ第2弾、横の移動について徹底解説していきます！

# おさらい
さて、前回はVimの4つのモードについて解説しました。
その中で、**h, j, k, l** キーで移動できることについて軽ーく触れました。

hキーで左に一文字移動、lキーで右に一文字移動でしたね。

しかし、ちまちま一文字移動してたら日が暮れてしまいますね。
こんなんじゃVim使ってドヤれません。 

今回は、もっと早い横への移動方法を3つ、ご紹介します。

# 横の移動その1: 回数を指定する
Vimでは、 **移動コマンドの前に回数を指定** することができます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/5l10h.gif" %}

例えば、`l`を使って右に移動する場合、`10l`と打つと右に10文字移動できます。
l押しっぱなしにするよりちょっと早いですね。

しかし、回数が指定できるからと言って、「移動したい文字ってここから何文字だろう」ってなりますよね。

例えば、「文末の句点はここから何文字だろう」なんて考えてると辛いものがあります。
文字をいちいち数えてるとかえって遅いですよね。なので、これはあまり使われないです。

# 横の移動その2: 単語で移動
Vimでは、`w`で次の単語に移動し、`b`で後ろの単語に移動できます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/wandb.gif" %}

これ、英語を使ってる場合は有用です。`h`と`l`を連打するよりちょっと早くなります。
また、このコマンドも回数指定できるので `3w`で三つ先の単語に移動できたりします。

英語の場合、単語は空白で区切られてるので見分けがつきやすいですよね。パッと近くの単語に移動したい場合に便利です。

問題は日本語を使ってる場合。一応、Vimは日本語が申し訳程度にわかるみたいで、それなりに単語を横断していきます。しかし、その精度はお世辞にもいいとは言えないです。しかも、日本語はスペースの概念がないので回数指定が難しい。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/wandb_japanese.gif" %}

Vimで英語書いてる時はよく使うコマンドです！

# 横の移動その3: 文字を検索
Vimでは、`f`で先の文字を検索し、`F`で後ろの文字を検索できます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/fpFA.gif" %}

`f`ind の `f` ですね。

`f`または`F`を打った後に移動したい文字を打つと、その文字に移動してくれます。

また、行の中に検索した文字が複数ある場合は、`;`で次のヒットに移動、`,`で後ろのヒットに移動できます。

これがすごく便利で、横移動はもっぱらこれで行います。文字は指定が楽なので、字数や単語数で移動するより簡単ですし、一度に移動できる距離も長いです。

# その他使えるやつ
## 行端への移動
- `0`で行の先頭に移動できます
- `_`で行の先頭の文字に移動できます
- `$`で行の末尾に移動できます
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/zero_$.gif" %}

行端に移動することは頻繁にあるので、移動を早くしてくれるこれらは覚えておいて損はないです！

# ビジュアルモード中の移動
今日紹介した移動コマンドは、ビジュアルモード中にも使えます！

- `vfy` -> 次のyまで選択
- `d3b` -> 後ろ3つの単語を削除
- `yFo` -> 後ろのoまでコピー
- `d$`行の末尾まで削除

{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-02-28-Vim-Nyuumon-2/tricks.gif" %}

このように、今日紹介した横の移動だけでも、編集コマンドとの組み合わせは多彩にあります！
コンビネーションを駆使できればどんどん編集スピードが速くなりますよ！

# 終わりに
この記事では、Vimでの横の移動について紹介しました！

次回は縦の移動について詳しく掘り下げていきます!

