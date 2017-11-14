---
layout: post
title: What are the Username and Hostname ?
subtitle: "USERNAME@HOSTNAME : PATH SYMBOL"
category: Linux
tags: [summary]
permalink: /2017/11/14/What_are_the_Username_and_Hostname/
---

# What does username@hostname in terminal?

If you basically open terminal, it looks like by defualt "[USERNAME]@[HOSTNAME]:[PATH][SYMBOL]"

In my environment of ubuntu linux, the terminal looks as follows :

![](/img/Image/Linux/2017-11-14-What_are_the_Username_and_Hostname/Terminal.png)

Formally, shell prompt looks like "[USERNAME]@[HOSTNAME]:[PATH][SYMBOL]" as you could read above.

let's Exactly go through what each of shell prompt means below :

- [USERNAME] : in my case, It is hyunyoung2, whenever you log in linux, you can see it. i.e. the username of the currently operating user. Basically this is you as current user in linux, BUT when you enter **su** mode, you get **root shell**,it means currently operating user is **root.**

- [HOSTNAME] : in my case, It is hyunyoung2-desktopter, so this is my hostname. that is to say, it's the name of your computer, another way is your ip address.

- [PATH] : in my case, It appear to be **in ~ **, So PATH is **~** by default in here, specifically speaking, It is your current working directory that you're currently operating on. So when you open a new terminal, the default directory is your current user's **home directory.** a synonym for  /home/YOURUSERNAME is ~ in linux.

- [SYMBOL] : in my case, It is **$** sign. BUT It basically either $ if you're operating as **any normal user**, or # if you're operating as **root** user.

once again look my case :

![](/img/Image/Linux/2017-11-14-What_are_the_Username_and_Hostname/Terminal.png)

 That means I logged in as user **hyunyoung2** on my linux computer called **hyunyoung2-desktop**. and Currently operating in my own home directory(~). Of course you're not **root**, Therefore the SYMBOL is **$**


# Reference 

  - [ask ubuntu](https://askubuntu.com/questions/6114/what-does-the-name-after-at-terminal-prompt-mean)
