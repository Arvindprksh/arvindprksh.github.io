---
layout: post
title: Linux File Permission
subtitle: What is "ls" command's meaning and File Permission in Linux 
category: Linux
tags: [linux, concept]
permalink: /2016/03/07/Linux_File_Permission/
---

now I will look into kernel's lightnvm ioctl(Input Output control, in short), so while studying kernel, I make a note that I learn.

Second Lesson 

1-1. ls  means list  directory contents

   I typed "ls -l" in linux computer. for example, The following result is 
   
```
dr-xr-xr-x.   5 root root    4096  4??  1 19:43 boot

drwxr-xr-x   20 root root    3260  8?? 26 10:24 dev

drwxr-xr-x. 153 root root   12288  8?? 27 11:53 etc

drwxr-xr-x.   6 root root     103  7??  6 16:09 home

lrwxrwxrwx.   1 root root       7  4??  1 16:46 lib -> usr/lib

[출처] [LINUX] ls -l 명령어 사용시 맨 앞에 나오는 파일 타입|작성자 b1ix
```
   
first letter of above result is directory's & file's type.

by default Unix have Only 3 type of file 

they are :

  - regular file (-)
  
  - directory file (d)

  -the following is special file type.
  1. Block file(b)
  2.  Character device file(c)
  3.  Named pipe file or just a pipe file(p)
  4.  Symbolic link file(l)
  5.  Socket file(s)


you want to know more. please refer to  <a href = "http://www.linuxnix.com/file-types-in-linux/"> linuxnix </a>

---

the following refer to <a href = "http://www.csit.parkland.edu/~smauney/csc128/permissions_and_links.html">csit.parkland</a>

now I am introducing file permission in linux.

so to check up Permissions, you use "ls -l",above linux command.

the ls -l command displays a lot of information about the files in the directory

![](/img/Image/Linux/2016-03-07-Linux_File_Permission/file_permissions.jpg)

so you need each permision to read, write and excute.

In other words, 

To read a file, you need to have read(r) permission for that file.

To write to a file, to modify a file, or to erase a file, yo need to have write(w) for that file.

To run a program or to change to a diretory, you need to have excute(x) permission for that program or directory.

![](/img/Image/Linux/2016-03-07-Linux_File_Permission/PermissionsConcept.png)

above picture refer to <a href = "http://www.guru99.com/file-permissions.html">guru99</a>
