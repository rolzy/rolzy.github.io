---
title:  "Vim入門① - 4つのモード"
date:   2024-01-07 00:00:00 +1000
tags: Vim 日本語
read_time: false
comments: true
classes: wide
toc: true
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png

---

# はじめに
2024年、Vimも今年で33歳（派生元のViは48歳)になるわけですが、いまさらVim入門シリーズを書きたいと思います!

ソフトウェア開発、Webデザイナ、Vimに興味がある方は是非！

## Vimって何
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-01-28-vim-nyuumon-1/vim_screen.png" alt="私のVim画面" caption="私のVim画面" %}

Vimとはターミナルで動くテキストエディタです。

これ使えば、どんなファイルでもチョチョイと編集できちゃいます。ターミナルで動くのでチョー軽いです。

しかも大抵のLinuxマシンに入ってるので、他サーバーにSSH接続したときとかでもすぐ起動できます。リモートデスクトップなんていらねぇ。

これ使いこなせると、~~周囲からヲタク認定~~スーパーハカーとして崇められること請け合いです。

### Vim vs Vim動作
でもこいつ、ターミナルで動くので、とっつきにくい見た目をしてます。

UI/UXのユの字もありません。

でも大丈夫！ホンモノのVimを使わなくても、Vim動作さえ覚えちゃえば君の好きなIDEでVimが使えます。

というのも、VSCode, IntelliJ, PyCharm, Eclipseなど大抵のIDEにはVimモードが備え付きorエクステで手に入るからです。

逆に言えば、Vim動作はいろんなIDEに取り入れられるほど人気なのです。かくいう僕も、Vimなしでは物が書けない体になってしまいました。 今もこの記事をセコセコVimで書いてます。

そんな大人気なVimなので、ぜひ使えるようになりましょう!

{% capture notice-text1 %}
IDEからVimモードを使う場合は、エクステンションをインストールしてあげてください。
有名なIDEのVimエクステンションを張っておきます: 
- [VSCode](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) 
- [IntelliJ/PyCharm](https://plugins.jetbrains.com/plugin/164-ideavim)

「載ってないよー😭」って方は **"[IDEの名前] VIM"** でググれば出てくるはずです。
{% endcapture %}

<div class="notice--info">
  <h4 class="no_toc">エクステンションのインストール</h4>
  {{ notice-text1 | markdownify }}
</div>

{% capture notice-text2 %}
本物のVimを使いたい猛者の方はターミナル環境が必要になります。
これはお使いのOSによって異なります。OS別のおすすめインストール方法を載せておきますね。
- Windows: `gVim`というプログラムをインストールすると、コマンドプロンプトとPowerShellからVimが使えるようになります。詳しくは[こちら](https://web.yokkaichi-u.ac.jp/yucc/archives/2205)
- Mac: ターミナルを開いて`brew install vim`
- Linux: お使いのディストロのPackage Managerからインストールしてください。例: Debian/Ubuntuの場合は `apt install vim` ですね。
{% endcapture %}

<div class="notice--warning">
  <h4 class="no_toc">ホンモノのインストール</h4>
  {{ notice-text2 | markdownify }}
</div>

### Vimを起動してみよう
Vimがインストールできたら、早速起動してみましょう。
起動方法はソフトウェアによって異なります。

**IDEの場合**
エクステンションをインストールしたら、自動的にVimモードがオンになってるはずです。
IDEの画面下に **--NORMAL--** みたいな表記があったら読み込み成功です。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-01-28-vim-nyuumon-1/vim_on_vscode.png" alt="VSCode上のVim" %}

**ターミナルの場合**
Vimコマンドをインストールしたら、`vim <ファイル名>`でVimを起動できます。
{% include figure image_path="https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/general-images/2024-01-28-vim-nyuumon-1/vanilla-vim.png" alt="バニラVim" %}
 


## このシリーズの構成
このシリーズでは、Vimを下記の6種類に分けて一つずつ紹介していきます。
- 4つのモードについて <- 今ココ
- 横の移動
- 縦の移動
- 文章の編集
- コンビネーション
- 上級テクニック

Vimってできることが多いので、最初から全部覚えようとすると大変です。
一つずつ、じっくりと学んでいきましょう。

**最初が一番難しい!**
Vimはマウスとか取っ払ってキーボードだけで操作を簡潔させるプログラムです。
マウスを使った移動や文章の選択は一切行いません!
これまで使い慣れたマウスを手放すのはとても難しいでしょう。僕もそうでした。
でも、ちょっとずつ使っていけばVimの良さが分かってくると思うので、頑張っていきましょう！
{: .notice--info}

___ 

# 4つのモード
ということで、本記事ではVim内の「モード」について解説します。
下記の4つです。
- インサートモード (Insert mode): 文章が書けます
- ノーマルモード (Normal mode): カーソルを移動できます
- ビジュアルモード (Visual mode): 文章を選択できます
- コマンドモード (Command mode): コマンドを動かします

一つずつ見ていきましょう！

## インサートモード (Insert mode)
文章を書くモードです。Vimを起動した後、`i`nsertの`i`を押すとこのモードに入ります。

Wordみたいに、タイプした文字がそのまま表示されるようになります。 試しにいろいろ書いてみましょう!

## ノーマルモード
カーソルを移動するときに使うモードです。実はこれデフォルトのモードで、Vim起動するとこのモードで始まります。

さっき`i`を押したのも、ノーマルモードからインサートモードに入るためです。

他のモードからノーマルモードに切り替えるには、`Esc`キーを押します。

そうすると、カーソルを `h`(左), `j`(下), `k`(上), `l`(右)で動かせるようになります。

**矢印は使っちゃダメ!**
矢印でもカーソルの移動はできますが、推奨しません。キーボードの中央から遠いからです。
両手は極力キーボードに添えたままテキスト編集できるのがVimの真骨頂です。
Vimを使いこなしたければ、矢印キーは捨てましょう。
{: .notice--warning}

## ビジュアルモード
文章を選択するときに使うモードです。

ノーマルモードから`v`isualの`v`を押すとこのモードに入ります。

ビジュアルモードではノーマルモードと同じ`hjkl`の移動コマンドが使えます。
試しにカーソルを動かすと、文章がハイライトされていくのがわかると思います。

さらに、ハイライトされた文章のコピーや削除もこのモードでできます。
- 文章がハイライトされた状態で`d`を押すと、選択された文章を切り取ります。(`d`eleteの`d`)
- 文章がハイライトされた状態で`y`を押すと、選択された文章をコピーします。(`y`ankの`y`)
- 文章を切り取り・コピーした後に`p`を押すと、カーソルの位置に文章を貼り付けます。(`p`asteの`p`)

## コマンドモード
ファイルの保存やVimの終了など、プログラムの操作に使うモードです。

ノーマルモードから`:`と押すとこのモードに移行し、画面下記に文字をタイプできるようになります。
- ノーマルモードから`:w`と打つと、ファイルの保存を行います。(`w`riteの`w`)
- ノーマルモードから`:q`と打つと、Vimを終了します。(`q`uitの`q`)
- 2つ合わせて`:wq`でファイルを保存してから終了できます。

**Vimから出れる!**
おめでとうございます、これであなたもVimから出れるようになりましたね!
初心者が陥りやすい罠で、Vim入ったけど出れないってことはよくあります。私もやらかしたことあります。
実はこの現象、海外ではちょっとした[ネットミーム](https://thenewstack.io/how-do-you-exit-vim-a-newbie-question-turned-tech-meme/)なんですよ。
{: .notice}

これは初歩的な記事なので列挙しませんが、コマンドモードではマジでいろんな操作ができます。
もっと詳しく知りたい方は[こちら](https://vim-jp.org/vimdoc-ja/vimindex.html#ex-cmd-index)からどうぞ!

# おわりに
この記事では、Vimの4つのモードの解説と、それぞれの初歩的な操作を紹介しました。

ホントは各モードで紹介したい操作がいっぱいあるんですが、取り上げすぎると頭こんがらがっちゃうので次回以降に取っておきます。
まずは基本のVim起動 -> ファイル書き込み -> 切り取り・貼り付け -> ファイルの保存 まで紹介しました。

次回は横の移動について詳しく掘り下げていきます!
