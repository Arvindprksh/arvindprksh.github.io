---
layout: post
title: Organization of vim command
subtitle: During researching natural lanuage with Ubuntu, organizing what I have known vim command.
category: Natural Language Processing Labs
tags: [linux, vim]
permalink: /2018/01/17/Vim_command/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

 Here to get used to Vim, I will organize what I have known about vim command. trying to get information of the commands. 
 
 I did already it. But from now on I will do in detail once again here to get used to it. 
 
 First, Let's see how to copy and paste texts or lines.
 
# [Copy and Paste in Vim](http://vim.wikia.com/wiki/Copy,_cut_and_paste)
 
 Basically, If you want to copy and paste in vim, remember three keywords, d, y, p
 
  - **d** stands for *delete* in Vim, which in other editor is usually called *cut* 
  
  - **y** stands for *yank* in Vim, which in other editor is usually called *copy*
  
  - **p** means putting the text after the cursor where you are currently. 
 
Let's go through two ways of "copy and paste" and "cut and paste"  
 
## Copy and Paste with a line in Vim
 
  - **yy or Y** - yank the current line including the newline character at the end of the line 
  
  - **p** - put the text after the cursor where you are currently. 
 
  - **P** - put the text before the cursor where you are currently.
  
## Cut and paste using visual selection in Vim 

First, let's go through how to select text or line using visual selection in Vim. 

the key word of visual selection is **v** and **V**
 
 - **v** - Select character
 
 - **V** - Select whole line
 
 - **Ctrl+v** - Select rectangular blocks
 
If you choose a block to copy with visual selection, from now on, it is the same from copy and paste with a line in Vim. 

In the position of what you want to cut, 

 1. Press **d** to cut ( or **y** to copy)
 
 2. Move to where you would like to paste
 
 3. Press **P** to paster before the cursor, or **p** to paste after the cursor. 
 
those is it about how to cut and paste using visual selection. 
 
# [Search for text or the number of line you want](http://vim.wikia.com/wiki/Searching)

you have to search for text you want in command mode of vim. 

Basically, Let's see key words of search in vim. in Command mode, press **/** or **?**

 - **/** - Search forwards for the pattern you will type after **/**
 
 - **?** - Search backwords for the pateren you will type after **?**
 
 To navigate continuously searh for the pattern, Press **n** or **N**
 
 - **n** - Search forwards if you type some pattern with **/**. if you type some patter with **?** , Search backwards.
 
 - **N** - This is vice versa in the case with **/**, search backwards, in other way of **?**, Search forwards. 
 
## Search for the current word in Vim 
 
If you would like to search for the current work, move the cursor to any word you want to search for. 

Press __*__ to search forwards for the next occurrence of that word, or Press **#** to search backwards.
 
__*__, **#** - Search for the exact word at the cursor like : 

If you search for **rain**, it would not find out **rainbow**
 
But when you type subword of a whole word, If you want to find a whole word including subword.

Use **g** if you don't want to search for the exact word like __g*__, **g#**

## How to see cp949 or another encoded character on vim

> e ++ecn=<your text's encoding>   
> e ++enc=cp949

## How to execute code in vim window 

go to command mode by pressing <esc> key and type:

> ! clear; python3 %

step by step about explanation of the command 

**!**: allows you to run a termainal command 

**clear**: will empty your terminal screen 

**;**: ends the first command, allowing you to introduce a second command

**python3**: will you python3 to run your script (it could be replaced with ruby for example)

**%**: concats the current filename, passing it as a parameter to the python command

## [How to set current line and column](https://coderwall.com/p/adbciq/highlight-line-and-column-in-vim)

If you want to represent current line and columns in vim. 

set confirguration below in vimrc file.

> set cursorcolumns # highlight current line   
> set cursorline # highlight current column

If you give [cursorline and cursorcolumn an effect](https://stackoverflow.com/questions/8640276/how-do-i-change-my-vim-highlight-line-to-not-be-an-underline) like bold 

type in the following option in vimrc file 

> highlight-Cursorcolumn-cterm=bold   
> highlight-Cursorline-cterm=bold

## [How to set tab sign with '|'](https://stackoverflow.com/questions/41206522/how-can-i-display-tab-as-bars-in-vim)

If you want to set tab setting consisting of two character **|** and a space. 

> set list lcs=tab:\|\ #the last character is space!

but if you want to change a sapce into another character. 

set as follows

> set list listchars=tab:\|\- 

## [How to set white-space sign with another character](https://stackoverflow.com/questions/40498265/show-space-character-via-listchars-only-for-leading-spaces)

If you want to see the white-space character, 

> set list listchars=space:-

# Reference
 
  - [Searching in Vim](http://vim.wikia.com/wiki/Searching)
  
  - [copy and paste](http://vim.wikia.com/wiki/Copy,_cut_and_paste)
  
  - [how to execute code in vim windown](https://stackoverflow.com/questions/18948491/running-python-code-in-vim)
  
  - [How to set current line and column](https://vim.fandom.com/wiki/Highlight_current_line)
  
  - [How do I change my Vim highlight line to not be an underline on stackoverflow](https://stackoverflow.com/questions/8640276/how-do-i-change-my-vim-highlight-line-to-not-be-an-underline)

  - [How to set tab sign with '|'](https://stackoverflow.com/questions/41206522/how-can-i-display-tab-as-bars-in-vim)
  
  - [How to set white-space sign with another character](https://stackoverflow.com/questions/40498265/show-space-character-via-listchars-only-for-leading-spaces)
  
