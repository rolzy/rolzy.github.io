---
title:  "Shorten Frequent Commands with Alias and Functions"
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

In this article I will explain `alias` and `function` in shell scripting. After you
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

## Limitations
Aliases are good and all, but how about if we want to send it parameters?
For example, say we defined the following alias:

`alias la='ls -la'`

and then we want to look in a particular directory. 

# Functions
<!-- 
- Limitations
    - Can't pass arguments
    - Say we want to pass a string during runtime, but shorten the command itself
- Functions
    - I want to pass arguments to the commands
    - What is an function
    - Also set it in .rc file
- Conclusion
    - 
-->
