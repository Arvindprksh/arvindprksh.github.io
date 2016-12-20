---
layout: post
title: Basic Shell Command & Software Package
subtitle: summary of shell command
category: Linux
tags: [linux, command, concept]
permalink: /2016/04/01/Basic_Shell_Command/
---

this refers to <a href = "https://www.linux.com/learn/tutorials/819973-how-to-use-the-linux-command-line-basics-of-cli">linux's tutorial</a> 


# Get the Shell

Shell is basically a program that turns the "text" that you type into commands/orders for your computer to perform.

As such there is a set structure of commands, differenct OSes may use a different structure to perform the same task.

There are many Shells available for Linux, but the most popular is Bash(Bourne-Again shell) which was written by the GNU Project.

If you are using a desktop enviroment then you need a terminal emulator to emulate the thr terminal within that interface. 

Different distros come with their own terminal emulators.

# Basics Commands

When you open a terminal emulator, by default you are in the home directory of the logged in user. 

Your will see the name of the logged in user followed by the hostnam. $ means you are logged in as a regular user, wherea # means you are logged in as root.

unless you are perfoming administrative tasks or working inside root directories, never work as root becuase it will change the permission of all directories and files you worked on.

you can list all directories and files inside the current directory by using the ls command. 

```shell
[hyunyoung.lee@localhost ~]$ ls
Desktop    Downloads  linux-4.5         Music     Public     Videos
Documents  leveldb    linux-4.5.tar.xz  Pictures  Templates
```

## cd

To change to any directory, use the cd command. You cas also use the 'Tab' key which will auto completes the path. 

use forward slash to enter directories. So if I want to chage directory to 'Downloads' which is inside my home folder, we run cd and then give the path.

In this case, 'hyunyoung.lee' is the username. You need to type your usename.

```shell
[hyunyoung.lee@localhost ~]$ cd /home/hyunyoung.lee/Downloads/
[hyunyoung.lee@localhost Downloads]$ 
```

As you can see in the second line, 'Downloads' diretory has moved inside the square brackets, which denotes that currently we are inside this directory. 

I can see all subdirectories and files inside Downloads directory by running the ls command.

You don't have to give the complete path if you want to move inside the sub-dictrectory of the current directory. Just type cd and the directory name..

If you want to move to another directory just follow the same pattern : cd PATH_OF_DIRECTORY.

If you want to move one step back in the directory then use "cd .." to go back two directories, use "cd ../.." and so on.

But if you want to get our of the current directory and go back to home simply type cd.

## ls 

You don't have to change directory to see its content. You can use the ls command in following manner :

ls /PATH_OF_DIRECTORY

To see hidden directories and files use -a option with the ls command.

ls -a /PATH_OF_DIRECTORY

So as to sse the size of directories and files you can use -l option with the ls command. It will also tell the permissions of the files and directories, their owners and the time/data of modification:

```shell
[hyunyoung.lee@localhost ~]$ ls -l
total 86312
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Desktop
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Documents
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 13:53 Downloads
drwxrwxr-x. 13 hyunyoung.lee hyunyoung.lee     4096 Apr  1 14:30 leveldb
drwxrwxr-x. 24 hyunyoung.lee hyunyoung.lee     4096 Mar 13 21:28 linux-4.5
-rw-rw-r--.  1 hyunyoung.lee hyunyoung.lee 88375040 Apr  1 13:53 linux-4.5.tar.xz
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Music
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Pictures
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Public
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Templates
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee        6 Apr  1 11:31 Videos
```

the command gave us the file size in a form hard to understand. If you want to get the file size in human readable format then use ls -lh command.

```shell
[hyunyoung.lee@localhost ~]$ ls -lh
total 85M
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Desktop
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Documents
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 13:53 Downloads
drwxrwxr-x. 13 hyunyoung.lee hyunyoung.lee 4.0K Apr  1 14:30 leveldb
drwxrwxr-x. 24 hyunyoung.lee hyunyoung.lee 4.0K Mar 13 21:28 linux-4.5
-rw-rw-r--.  1 hyunyoung.lee hyunyoung.lee  85M Apr  1 13:53 linux-4.5.tar.xz
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Music
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Pictures
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Public
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Templates
drwxr-xr-x.  2 hyunyoung.lee hyunyoung.lee    6 Apr  1 11:31 Videos
```

## mkdir

if you want to create new directories, the command is 'mkdir'. by default the directory will be created in the current directory. 

So give the complete path of the location where you want the directory to be created

mkdir /PATH-OF-THE-PARENT-DIRECTORY/NAME-OF-THE-NEW-DIRECTORY

So if I want to create a directory 'distros' inside the 'Downloads' directory. then this is the command I will run :

```shell
[hyunyoung.lee@localhost ~]$ mkdir /home/hyunyoung.lee/Downloads/distro
[hyunyoung.lee@localhost ~]$ ls
Desktop    Downloads  linux-4.5         Music     Public     Videos
Documents  leveldb    linux-4.5.tar.xz  Pictures  Templates
[hyunyoung.lee@localhost ~]$ cd D
Desktop/   Documents/ Downloads/ 
[hyunyoung.lee@localhost ~]$ cd Downloads/
[hyunyoung.lee@localhost Downloads]$ ls
distro
```

If you want to create a sub-directory inside a new and current directory then use '-p' option with 'mkdir'. 

```shell
[hyunyoung.lee@localhost ~]$ mkdir -p dsf
[hyunyoung.lee@localhost ~]$ ls
Desktop    Downloads  leveldb    linux-4.5.tar.xz  Pictures  Templates
Documents  dsf        linux-4.5  Music             Public    Videos
[hyunyoung.lee@localhost ~]$ 
```


## rm

If you want to delete any file or directory, the command is 'rm(for file)' and 'rm -r(for directory)'. 

You need to be very careful with this command because if you fail to give the correct path of the file or directory the it will remove everything from the current directory and you may lose precious data.

The command is simple

rm /PATH-OF-THE DIRECTORY-OR-FILE

the following refers to <a href ="https://www.linux.com/learn/tutorials/821646-break-the-gui-software-management-from-the-command-line">Linux's tutorial</a>

In linux, to manage software, you have to tool like apt-get, aptitude, yum.


## chmod

to have privilege sudo, I configured /etc/sudoers file.

instruction :

```
  $ su  
  password :
  $ chmod u+w /etc/sudoers
  $ vim etc/sudoers
  $ chmod u-w /etc/sudoers
```

these instructions are processed by linux system.

now. I will notice that chmod, sudoes file and so on. 


# .a file & .so file

  
.a - static library
.so - dynamic library

this refers to <a href = "http://stackoverflow.com/questions/9809213/what-are-a-and-so-files">stackoverflow</a>

Archive libraries (.a) are statically linked i.e when you compile your program with -c option in gcc. So, if there's any change in library, you need to compile and build your code again.

The advantage of .so (shared object) over .a library is that they are linked during the runtime i.e. after creation of your .o file -o option in gcc. So, if there's any change in .so file, you don't need to recompile your main program. But make sure that your main program is linked to the new .so file with ln command.

if you know more about library in linux, please refer to <a href = "http://www.ibm.com/developerworks/library/l-dynamic-libraries/">l-dynamic-libraries site</a>

# Basic yum packages

yum is standard package for management software on centos. so you don't confuse apt-ooo related to ubuntu.

refer to <a href ="http://unix.stackexchange.com/questions/75279/finding-yum-equivalents-of-apt-repositories">stackexchange.</a>
