---
layout: post
title: Benchmark tool of filesystem - filebench
subtitle: How can I test filesystem with filebench
category: SSD (Solid State Drives)
tags: [filesystem, benchmark]
permalink: /2016/12/23/Benchmark_Of_filebench/
---

 As you can read [my blog](/2016/12/12/How_To_Check_Performance_Of_F2FS/), F2FS filesystem use filebench tool to verify filesystem.
 
 **So I need to this tool to verify the new f2fs filesystem.**
 
 this new f2fs is sequential about meta data and inode data. 
 
 
 
 
 
 
 
 ## Summary of command to build filebench.
 
 way to build filebench from officail site
 
 Because [file bench's repository](https://github.com/filebench/filebench) doesn't have configure file. 
 
 you have to generate the configure file. 
 
 
 
 

this version is another way. 

```shell 
$ git clone https://github.com/zfsonlinux/filebench.git
$ cd filebench
$ ./configure    -- run shell
$ make
$ sudo make install -- with sudo
$ filebench
$ set $dir=<dir>  -- in here, <dir> is formatted filesystem.
$ run 10
```

in my case, when I use the above commands, I got warning during building filebench
 
 
 ## Reference
 
  - 
 
  - [Way to build filebench](https://github.com/filebench/filebench/wiki)
 
  - [Way to compile filebench](https://github.com/zfsonlinux/filebench)
