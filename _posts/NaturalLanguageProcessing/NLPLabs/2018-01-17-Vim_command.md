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

# Reference
 
  - [Searching in Vim](http://vim.wikia.com/wiki/Searching)
  
  - [copy and paste](http://vim.wikia.com/wiki/Copy,_cut_and_paste)
