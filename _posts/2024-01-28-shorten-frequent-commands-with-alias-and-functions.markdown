---
title:  "Shorten Frequent Commands with Alias"
date:   2024-01-29 00:00:00 +1000
tags: 
  - Linux
  - Shell Scripting
comments: true
classes: wide
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png
---
# Introduction
When using Linux on the terminal, there are commands that we use frequently. 
Most of them are short to type out, like `cd`, `ls` or `rm`. 

But I'm sure we all have some commands that are very long, and yet we have no trouble
typing it out because we run it so often. Or, you may have commands where you add
the same arguments every time to the point where you want that argument to be the 
default.

In this article I will explain what `alias` are in shell scripting. After you
try this out, you will be able to save a lot of time from typing out commands!

# Alias
An `alias` in Linux is a user-defined shortcut for longer commands. 

To setup an alias, you use the `alias` command (surprise!).
The command takes the following format:

`alias [New and short command]=[Old and long command]`

For example, say you want a new `ls` alias with specific parameters. You might do something like this:

```
rolzy ~/projects/temp $ alias la='ls -la'
rolzy ~/projects/temp $ la
total 5020
drwxr-xr-x 13 rolzy rolzy    4096 Jan 23 18:05 .
drwxr-xr-x 18 rolzy rolzy    4096 Dec  8 16:16 ..
-rw-r--r--  1 rolzy rolzy       7 Jul 12  2023 .python-version
-rw-r--r--  1 rolzy rolzy    1931 Jan 23 18:05 temp
```

And voila! You can now type out `la` and save 4 keystrokes.

## Examples
Here are some aliases that I setup. They are all long commands that I run frequently.

```
alias python="python3"
alias gs='git status'
alias push='git push'
alias pull='git pull'
alias sa='source env/bin/activate'
```

## Sessions
One thing to note is that aliases are session-bound. Once you exit out of your terminal, your aliases will be gone as well. 
To get your alias back, you will have to run the `alias` command again.

To have your aliases on every session, I recommend you to setup your aliases in your `.rc` files. 
These files run at the beginning of every session. If you have your aliases defined in there,
 it will be setup and ready to go every time you start a new terminal session.

Your `.rc` file will depend on the shell you are using. 
- If you're using bash, your .rc file will be `~/.bashrc`.
- If you're using zsh, your .rc file will be `~/.zshrc`.

## Arguments
You can also send arguments to aliases as well. For example, if you have 

`alias la='ls -la'`

already setup, you can then pass in arguments to the command! 

For example, `la test_dir` will be the equivalent to `ls -la test_dir`.

With this in mind, I like to set some git related commands like these:

```
alias gd="git diff"
alias ga="git add"
alias gcm="git commit -m"
```

and then run a set of git commands like this:

`git diff test.py` becomes `gd test.py`

`git add -p test.py` becomes `ga -p test.py`

`git diff --staged test.py` becomes `gd --staged test.py`

`git commit -m "Make some changes to test.py"` becomes `gcm "Make some changes to test.py"`

## Conclusion
And thats it! If you have any aliases that you use, let us know in the comments :)
