---
layout: post
title: Git and Oh My Zsh
subtitle: What is Git ? And A useful git site that I can understand, 
category: Linux
tags: [git, shell]
permalink: /2016/10/11/Git_And_Oh_my_Zsh/
---

## practice site of github

  - [Codeacademy](https://www.codecademy.com/)

    you can practice basic function.  I alread did it.
        
  - this site is made of opensourc to practice git's basic functions.
     
     [practic site of English version](http://learngitbranching.js.org/)
 
     [practice site of Korean version](http://learnbranch.urigit.com/)
    
  - [Try Git: Git Tutorial](https://try.github.io/levels/1/challenges/1)
    

## Theory of git and github
  
  - The following shows you all github 
  
     [git book](https://www.gitbook.com/book/snowdream86/github-cheat-sheet/details)
  
  - the following is just korean language for explanation
  
     [theory of git](https://nolboo.kim/blog/2013/10/06/github-for-beginner/)

  - site you can easily understand.
  
     [theory of git](https://www.atlassian.com/git/tutorials/refs-and-the-reflog/)
     
  - [Github practice](http://www.slideshare.net/flyskykr/github-46014813)

## guid for git 

  1. [git - the simple guide](http://git.huit.harvard.edu/guide/)

  2. [collection site of git practice](https://github.com/grayghostvisuals/practice-git)
  
## how to see git_log 

  1. [Stackoverflow](http://stackoverflow.com/questions/1057564/pretty-git-branch-graphs)

## Practice and each command's summary.


## [z shell](http://ohmyz.sh/)

  ![](/img/Image/Linux/2016-10-11-Git_And_Oh_my_Zsh/Oh_my_zsh.png)
  
```bash
  $ sudo yum install zsh  
  $ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"  
  # For theme   
  $ vi .zshrc  
  $ zsh  
  $ exit or bash  
```

 on Ubuntu 16.04
 
```bash 
hyunyoung2@hyunyoung2-desktop:$ zsh
The program 'zsh' is currently not installed. You can install it by typing:
sudo apt install zsh
hyunyoung2@hyunyoung2-desktop:$ sudo apt-get install zsh
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  zsh-common
Suggested packages:
  zsh-doc
The following NEW packages will be installed:
  zsh zsh-common
0 upgraded, 2 newly installed, 0 to remove and 10 not upgraded.
Need to get 3,822 kB of archives.
hyunyoung2@hyunyoung2-desktop:$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
The program 'curl' is currently not installed. You can install it by typing:
sudo apt install curl
hyunyoung2@hyunyoung2-desktop:~/Downloads$ sudo apt-get install curl
Reading package lists... Done
Building dependency tree       
Reading state information... Done
........
Setting up curl (7.47.0-1ubuntu2.2) ...
hyunyoung2@hyunyoung2-desktop:$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
Cloning Oh My Zsh...
Cloning into '/home/hyunyoung2/.oh-my-zsh'...
remote: Counting objects: 831, done.
remote: Compressing objects: 100% (700/700), done.
remote: Total 831 (delta 14), reused 775 (delta 10), pack-reused 0
Receiving objects: 100% (831/831), 567.67 KiB | 104.00 KiB/s, done.
Resolving deltas: 100% (14/14), done.
Checking connectivity... done.
Looking for an existing zsh config...
Using the Oh My Zsh template file and adding it to ~/.zshrc
Time to change your default shell to zsh!
Password: 
         __                                     __   
  ____  / /_     ____ ___  __  __   ____  _____/ /_  
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \ 
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / / 
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/  
                        /____/                       ....is now installed!


Please look over the ~/.zshrc file to select plugins, themes, and options.

p.s. Follow us at https://twitter.com/ohmyzsh.

p.p.s. Get stickers and t-shirts at http://shop.planetargon.com.

➜  ~ 
```
 
 To sum up how to install zsh and extra tool as soon as you install Ubuntu, 
 
 in here my system Ubuntu is 16.04.1
 
 > uname -a
 
```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [22:03:08] 
$ uname -a
Linux hyunyoung2-desktop 4.8.0-36-generic #36~16.04.1-Ubuntu SMP Sun Feb 5 09:39:57 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux\
```
  
  Les't see the procedure of how to install zsh and additional tool
 
  when you use software package management in Ubutu, I recommend you to use apt instead of apt-get:
  
  if you want to know the reason why I recommend you to use apt, read pthis blog,Difference Between apt and apt-get explained.](https://itsfoss.com/apt-vs-apt-get-difference/)
  
  And then, if  you also want to know how to know how to Install Development Tools on Ubuntu, read [this blog, How To Install Development Tools on Ubuntu, Debian & LinuxMint.](https://tecadmin.net/install-development-tools-on-ubuntu/#)
 
````bash
# For development tools
$ sudo apt update 
$ sudo apt insatll build-essential 
# To check development tools is installed well
$ gcc --version
$ sudo apt insatll zsh
$ sudo apt install curl
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# To chang Theme on zsh
# In my case I changed robbyrussell to ys 
$ vim .zshrc
# To install vim editor(there are many vim packages, Some other people recommend vim-nox)
$ sudo apt install vim
```

 Just as additional explanation of vim package 

```bash 
# Just as appendix if you don't install vim type vim --version  like the following
$ vim --version
The program 'vim' can be found in the following packages:
 * vim
 * vim-gnome
 * vim-tiny
 * vim-athena
 * vim-athena-py2
 * vim-gnome-py2
 * vim-gtk
 * vim-gtk-py2
 * vim-gtk3
 * vim-gtk3-py2
 * vim-nox
 * vim-nox-py2
Try: sudo apt install <selected package>
# But if you have already installed vim. when you type $ vim --version like this :
$ vim --version
VIM - Vi IMproved 7.4 (2013 Aug 10, compiled Nov 24 2016 16:44:48)
.......
Compilation: gcc -c -I. -Iproto -DHAVE_CONFIG_H   -Wdate-time  -g -O2 -fPIE -fstack-protector-strong -Wformat -Werror=format-security -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1      
Linking: gcc   -Wl,-Bsymbolic-functions -fPIE -pie -Wl,-z,relro -Wl,-z,now -Wl,--as-needed -o vim        -lm -ltinfo -lnsl  -lselinux  -lacl -lattr -lgpm -ldl     -L/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu -lpython3.5m -lpthread -ldl -lutil -lm  
```

## [Oh my zsh's feature site](http://code.joejag.com/2014/why-zsh.html)

## [The Silver Search "ag"](https://github.com/ggreer/the_silver_searcher)

### How to install ag

  On My CentOS 7 
  
  > $ sduo yum install -y epel-release.noarch
  
  > $ sudo yum install -y the_silver_searcher
  
  If you want to know more, just refer to [the_silver_searcher git repository's README](https://github.com/ggreer/the_silver_searcher/blob/master/README.md)

## For example, In order to search  

  > $ ag "string or regular expression to search" -A 5 -B 5
  
  this means the result of ag is in front 5 line and back 5 line from string that ag find. 
  
# Reference 

 - [The Silver Search "ag"](https://github.com/ggreer/the_silver_searcher)


 - for studying of github.
   
   [NHN ent. 신승엽님 Github 실습 교육](http://www.slideshare.net/flyskykr/github-46014813)
  
 
