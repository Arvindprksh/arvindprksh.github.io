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


# [How To USe Bash History commands](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps) 

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

