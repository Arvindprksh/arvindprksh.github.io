---
layout: post
title: Organization Of Linux Commands
subtitle: during researching natural lanuage with Ubuntu, organizing Linux command.
category: Natural Language Processing Labs
tags: [linux, command]
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

If you don't know the command of linux, type in "man command" !

## [How To Uncompress A File With tar Command](https://askubuntu.com/questions/499807/how-to-unzip-tgz-file-using-the-terminal)

Basically, If you want to extract a .tgz file with tar command 

  > tar -xvzf /path/yourfile.tgz
  
  - x for extract
  - v for verbose
  - z for gnuzip
  - f for file, should come at last just before file name 

## [How To Count Words or Lines On linux Command](https://stackoverflow.com/questions/3137094/how-to-count-lines-in-a-document)

  For the number of line 
  
  >  wc -l file-name
  
  For counting words in a file 
  
  >  wc -w file-name 
  
  But if I want to count words in a line of a file. I use some shell script with wc like this. 
  
  > for i in 1; do read line ; echo $line; done < ./file-name | wc -w
  
## [How To Split A Document With The Number Of Lines You Want To Cut](https://stackoverflow.com/questions/19031144/how-to-split-one-text-file-into-multiple-txt-files)

 > split -l (the number of lines) input.txt output.txt

 - l : the number of lines you want to seperate 
 - input.txt : the name of a file to cut 
 - output.txt : file name you make after cuting input file. 
   - Normally if you don't specify the name of output file, the output is xaa, xab, xac, xad
   - But if you use prefix of the file name of output, like this 
   - e.g. if you type in split -l 1000 test.log test.log_
   - the result is test.log_aa, test.log_ab, test.log_ac, test.log_ad
   
 if you use -b option. -b means it seperate a file according to size with -b option. 


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

If you don't know Terminology about [MIME type](https://stackoverflow.com/questions/3828352/what-is-a-mime-type), See [this StackoverFlow](https://stackoverflow.com/questions/3828352/what-is-a-mime-type) wich is explaining it.

Namely, simply speaking of it, MIME stands for Multi-purpose Internet Mail Extensions. MIME types form a standard way of classifying file types on the Internet just like a label to identify a type of data. 

## [How To Chage An Encoding Into Another Encoding](https://stackoverflow.com/questions/64860/best-way-to-convert-text-files-between-character-sets)

For now, If you read the above How To Check A File Encoding On Linux, After that, You need to chang with some tool to help you.

It's [iconv](http://www.gnu.org/savannah-checkouts/gnu/libiconv/documentation/libiconv-1.15/iconv.1.html) tool. Let's See An example of usage of the tool, iconv.

 > iconv -f UTF-8 -t ISO-8859-15 in.txt > out.txt
 
 - \-f means the input file. 
 - \-t means the output file 

As you can read the above summary, It's simple to convert encoding. 

## [How to Write AWK Commands and Scripts](https://www.lifewire.com/write-awk-commands-and-scripts-2200573)

Let's see the AWK command, this command is a powerful method for porcessing or analyzing text files, In particular, like data files that are orgarnized by lines(rows) and columns.

> awk 'pattern {action}' input-file > output-file

This means that each line of the output file; if the line contains the pattern and awk apply the action to the line and write the resulting line to the output-file.

Let's think some sample.

> awk '{ print $5 }' table1.txt > output1.txt

The above command is under the situation where it doesn't contain the pattern. 

This means it takes fifth column of each line in input file of table1.txt and then it ouputs the resulting value to output file.

The whole process way is as followings :

BUT, keep in mind of one based, I mean first column is $1, the second one is $2 and so on. 
 
```
# This is table1.txt

1, Justin Timberlake, Title 545, Price $7.30
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $7.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $7.30
7, John Lennon, Title 271, Price $7.90
8, Michael Jackson, Title 373, Price $5.50
```

```
# This is ouput1.txt 

545,
723,
610,
118,
482,
335,
271,
373,
```

## [How To Use SED Command](http://endic.naver.com/search.nhn?sLn=en&searchOption=all&query=repetition)

let's see Sed command in Linux/Unix with examples.

SED command in UNIX stands for stream editor and it can perform  a lot of function on file like searching, finde and replace,  insertion or deletion. Though most common use of SED command in UNIX is for substitution for for find and replace. By using SED command, you can edit files even without opening it, which is much quicker way to find and replace something in file, than first opening that file in VI Editor and then changing it. 

To sum up:

  - SED is a powerful text stream editor. Can do insertion, deletion, search and replace 
   
  - SED command in unix supports regular expression which allows it perform comlex pattern matching.
  
**Syntax**

```
sed OPTION... [SCRIPT] [INPUTFILE...]
```

Let's set up test file like this: 

```shell# hyunyoung2 @ hyunyoung2-desktop in ~ [19:27:11] 
$ cat geekfile.txt 
unix is great os. unix is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

First example 

> $ sed "s/unix/linux/' geekfile.txt

Output : 

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [19:27:18] 
$ sed "s/unix/linux/" geekfile.txt 
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

Here the "s" specifies the substitution operation. The "/" is delimiter. so sed command replaces "unix" with "linux".

But, By default, sed command replaces the first occurence of the pattern in each line and it won't replace the second, third.. occurence in the line.

To raplace nth occurence of a pattern in a line. use /1 or /2 flag like this:

> $ sed "s/unix/linux/2" geekfile.txt

Output:

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [19:29:14] 
$ sed "s/unix/linux/2" geekfile.txt
unix is great os. linux is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.linux is a multiuser os.Learn unix .unix is a powerful.
```

If you want all occurence to be substituted. use "g"(global replacement) flag and then sed command will replace all the occurences of the string in the line.

Or If you wan to see korean ver, visit [here](https://wiki.kldp.org/HOWTO/html/Adv-Bash-Scr-HOWTO/x12718.html)

## [How To Use TR Command](https://www.thegeekstuff.com/2012/12/linux-tr-command/)

This command is so easy to tranlate the input into output. 

Let' see an example of how we use tr command in linux/unix.

As you already noticed what the tr means, tr stands for translate. 

**Syntax**

The syntax of tr command is: 

> $ tr [OPTOIN] [SET1] [SET2]

If both the SET1 and SET2 are specified and "-d" OPTION is not specified, then tr command will replace each characters in SET1 with each character in same poistion in SET2. 

Let's see so easy sample. 

```shell
 # hyunyoung2 @ hyunyoung2-desktop in ~ [18:22:04] 
$ tr abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ        
thegeekstuff
THEGEEKSTUFF
``` 
Another an example of joning all the line in a file into a single line

```shell
$ tr -s '\n' ' ' < file.txt
```

# [Type command](https://bash.cyberciti.biz/guide/Type_command)

Here, Let's go through type command in linux. 

The type command is used to find out What kind of type the command is among alias, file, builtin and so forth. 

let's look at an example :

> type ll and type pwd

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [10:19:18] 
$ type pwd
pwd is a shell builtin

# hyunyoung2 @ hyunyoung2-desktop in ~ [10:19:24] 
$ type ll
ll is an alias for ls -lh
```

as you can see the above things, type command displays information about command type. 

If you want to know what kind of type the command is, **$ type the name of commmand you want to know**

I recommend you to type in without -t option, that's why it is as follows:

an example below is the result for me to type in type command on bash

```shell
hyunyoung2@hyunyoung2-desktop:~$ type -t ll
alias

hyunyoung2@hyunyoung2-desktop:~$ type ll
ll is aliased to `ls -alF'

# hyunyoung2 @ hyunyoung2-desktop in ~ [10:34:15] 
$ type -t ll
zsh: bad option: -t
```

without -t option, you can know more detail about what kind of type it is?

BUT, with -t option, it is too bad to understand it. BUT If you know linux in detail. it is okay, 

So If you are beginner of linux, type in type command without -t option.

Also, zsh warn you -t when you use -t option, as you can see the last one above. 

It said **-t option is bad**

Also you can find out path about where command file is as follows

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [10:24:22] C:1
$ type -p ls
ls is /bin/ls

# hyunyoung2 @ hyunyoung2-desktop in ~ [10:24:25] 
$ type -p pwd
pwd is /bin/pwd
```

Keep in mind with -p option, the -p option is used to find of the name of the disk file (external command) would executed by the shell. It will return nothing if it is not a disk file. 

# [wget](https://www.gnu.org/software/wget/manual/html_node/Download-Options.html#Download-Options)

In linux, when you wan to download some file, use **wget** command. 

But here go through wget with -c option in detail

> $ wget -c URL

**-c**, **--continue** is to continue getting a partially-downloaded file. This is useful when you want to finish up a download started by a previous instance of Wget, or by another program. For examaple 

> $ wget -c ftp://path-to-file/filename.

Note that **-c** only works with FTP servers and with HTTP servers that support the *Range* header. 

Let's say you alread have a file of filname. In this moment you type in to download the file of filename again without **-c**. 

It would just download the remote file to filename.1, leaving the truncated filename alone.

On the other hand, If you use **-c** on this situation and the server does ont support continued dowdloading, wget restart the download from scratch and overwrite the existing file entirely.

But, Basically If you use **-c**, you can expect you will ask the server to continue the retrieval from an offset equal to the length of the local file. 

# Reference 

 - [How To Uncompress A File With tar Command](https://askubuntu.com/questions/499807/how-to-unzip-tgz-file-using-the-terminal)
 
 - [How To Count Words or Lines On linux Command](https://stackoverflow.com/questions/3137094/how-to-count-lines-in-a-document)

 - [How To Split A Document With The Number Of Line](https://stackoverflow.com/questions/19031144/how-to-split-one-text-file-into-multiple-txt-files)
 
   - [Korea ver. of split command](http://ggachi.ncity.net/TIP/7480)

 - [How To Use Bash History Commands](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps)
 
 - [How To Check A File Encoding On Linux](http://mindspill.net/computing/linux-notes/determine-and-change-file-character-encoding/)
 
   - [Appendix - MIME type](https://stackoverflow.com/questions/3828352/what-is-a-mime-type)
 
 - [How To Chage An Encoding Into Another Encoding](https://stackoverflow.com/questions/64860/best-way-to-convert-text-files-between-character-sets)

 - [How To Write AWK Commands and Scripts](https://www.lifewire.com/write-awk-commands-and-scripts-2200573)

 - [How To Use SED Command](http://endic.naver.com/search.nhn?sLn=en&searchOption=all&query=repetition)
 
 - [How To Use SED Command2](http://conqueringthecommandline.com/book/sed)
 
 - [How To Use TR Command](https://www.thegeekstuff.com/2012/12/linux-tr-command/)
 
 - [How To Use TR Command2](https://www.computerhope.com/unix/utr.htm)
 
 - [How To practice Regular Expression](https://regexr.com/)
 
 - [Type command](https://bash.cyberciti.biz/guide/Type_command)

 - [Man type command](http://linuxcommand.org/lc3_man_pages/typeh.html)
 
 - [Dwonload option of wget command](https://www.gnu.org/software/wget/manual/html_node/Download-Options.html#Download-Options)
