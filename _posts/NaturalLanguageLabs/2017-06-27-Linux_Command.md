---
layout: post
title: organization of linux command
subtitle: during researching natural lanuage with Ubuntu, organizing Linux command.
category: Natural Language Labs
tags: [linux]
permalink: /2017/6/27/Linux_Command/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


I organized several Linux command before, you can see them in here :

- [New Command Of linux](https://hyunyoung2.github.io/2017/01/11/New_Command_In_LINUX/)

- [Vi command and Linux Command2](https://hyunyoung2.github.io/2016/09/26/Vi_And_LInux_Commands/)

- [Linux Command](https://hyunyoung2.github.io/2016/03/02/Linux_Command/)

In here I will arrange command of Linux, because In order to practice TensorFlow, I have to use Linux again.


## [How To USe Bash History Commands](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps) 

  Basically, You used to run "history", 
  
  But In here **Ctrl + R**, only if you press **Ctrl + R**, move backwards in you command history. whether or not the command include letters in "bck-i-search: 
  
  > enter "Ctrl +  R"
  
```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:16:09] 
$ vim .zshrc
bck-i-search: s_
```
the following is one more time to press "Ctrl + R"

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:16:09] 
$ sudo apt-get install vim
bck-i-search: s_
```
Let's see if "Ctrl + R " means move backwards

 > history 

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:16:09] 
$ history                 
    1  cd ..
    2  vim .zshrc
    3  sudo apt-get install vim
    4  vim .zshrc
    5  exit
```
## [How To Check A File Encoding On Linux](http://mindspill.net/computing/linux-notes/determine-and-change-file-character-encoding/)

Lest's say if you worked about Korean languages on Windows system, Basically The encoding of Korean language is "euc-kr". So if you deal with a file edcoded with euc-kr on Linux, then you need to change encoding of the file, dealt with on Windosw system, into utf-8. Namely, just recommend you to use Unicode system on encoding.
  
Currently, let's see how to check encoding of a file you want to work with. For example, 

 > file [-bi] [filename]

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~ [3:43:03] 
$ file temp2.py    
temp2.py: C source, UTF-8 Unicode text

# hyunyoung2 @ hyunyoung2-desktop in ~ [3:43:09] 
$ file -i temp2.py 
temp2.py: text/x-c; charset=utf-8

# hyunyoung2 @ hyunyoung2-desktop in ~ [3:43:14] 
$ file -bi temp2.py
text/x-c; charset=utf-8
```
As you can see the above output of file command, you can check encoding of the file with file command. 

## [How To Chage An Encoding Into Another Encoding](https://stackoverflow.com/questions/64860/best-way-to-convert-text-files-between-character-sets)

For now, If you read the above How To Check A File Encoding On Linux, After that, You need to chang with some tool to help you.

It's [iconv](http://www.gnu.org/savannah-checkouts/gnu/libiconv/documentation/libiconv-1.15/iconv.1.html) tool. Let's See An example of usage of the tool, iconv.

 > iconv -f UTF-8 -t ISO-8859-15 in.txt > out.txt
 
 - \-f means the encoding of the input file. 
 - \-t means the encoding of the output file 

As you can read the above summary, It's simple to convert encoding. 



# Reference 

 - [How To Use Bash History Commands](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps)
 
 - [How To Check A File Encoding On Linux](http://mindspill.net/computing/linux-notes/determine-and-change-file-character-encoding/)
 
 - [How To Chage An Encoding Into Another Encoding](https://stackoverflow.com/questions/64860/best-way-to-convert-text-files-between-character-sets)
