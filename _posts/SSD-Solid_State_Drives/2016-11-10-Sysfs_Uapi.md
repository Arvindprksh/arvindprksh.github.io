---
layout: post
title: Sysfs and UAPI
subtitle: What is different between Sysfs and proc ? and What is the UAPI ?
css:
tags:
date:
big-image:
share-image:
permalink:
comments:
show-share:
big-image:
meta-title:
meta-description:
---

# [profs VS sysfs](http://unix.stackexchange.com/questions/4884/what-is-the-difference-between-procfs-and-sysfs)

 - In one word, sysfs is new edition of profs. the detail is as follows
 
 Just I quote [the StackExChange](http://unix.stackexchange.com/questions/4884/what-is-the-difference-between-procfs-and-sysfs)
 
 In the beginning, the way that programs found out about the running processes on the system was via directly reading proecess structures from the kernel memory (opening /dev/mem, and intepreting the raw data directly). This is how the very first 'ps' commands worked. over time. some information was made available via system calls.
 
 However, It is bad form  to expose system data directly to user-space vid /dev/mem, and It is uncomportable to be constantly creating new system calls every time you wanted to export some new piece of precess data, and so a newer method was created to access structured data for user-space applications to find out about process attributes. this was the /proc filesystem. with /proc, the interfaces and structures (directories and files) could be kept the same, even as the underlying data structures in the kernel changed.this was much less fragile than the earlier system. 
 
 The /proc filesystem was originally desinged to publish process information and a few ke system attributes, required by 'ps', 'top', 'free' and a few other system utilites. However, because it was easy to use (both from the kernel side and the user side), it became a dumping ground for a whole range of system informtion. Also, it started to gain read/write files, to be used to adjust settings and control the operation of the kernel or its various subsystem. However, the methodology of implementing control interfaces was ad-hoc, and /prc soon grew into a tangled mess. 
 
 The sysfs (or /sys filesystem) was designed to add structure to this mess and provide a uniform way to expose system information and control points (settable system and driver attributes) to user-space from the kernel. Now, the driver framework in the kernel automatically creates directories under /sys when drivers are registered, based on the driver type and the values in their data structures. This means that drivers of a particular type will all have the same elements exposed via sysfs.
 
 Many of the legacy system information and control points are still accessible in /proc, but all new busses and drivers should expose their info and control points via sysfs. 

# What is the UAPI directory in linux.

  I refer to this aticle from [Stack Exchange](http://stackoverflow.com/questions/18858190/whats-in-include-uapi-of-kernel-source-project) and [The lwn.net](https://lwn.net/Articles/507794/)

 Here, I will simply write what the UAPI is. If you need to know more. just refer to reference site about UAPI.
 
 **Simply speaking, the uapi folder is supposed to contain the user space API of the kernel.**  


# reference 

 - [sysfs](http://www.makelinux.net/books/lkd2/ch17lev1sec8)
 
 - [Linux kernel archive's sysfs](https://www.kernel.org/doc/Documentation/filesystems/sysfs.txt)

 - [Oracle](https://docs.oracle.com/cd/E37670_01/E41138/html/ol_sysfs.html)
 
 - [opensource](http://opensourceforu.com/2015/05/talking-to-the-kernel-through-sysfs/)
 
 - [Directory -/sys in linux](http://superuser.com/questions/794198/directory-sys-in-linux)
 
---
 for Uapi

  - [Stack Exchange](http://stackoverflow.com/questions/18858190/whats-in-include-uapi-of-kernel-source-project)
  
  - [the LWN.net](https://lwn.net/Articles/507794/)
