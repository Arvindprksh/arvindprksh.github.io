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
 
## What is the FileBench ?

 Filebench is a filesystem and storage benchmark that can generate a large variety of workloads. Unlike typical benchmarks it is extremely flexible and allows to specify application's I/O behavior using its extensive Workload Model Language(WML). Users can either describe desired workloads from scratch or use (with or without modifications) workload personalities shipped with filebench (e.g., mail-, web-, file- and database-server workloads). Filebench is equally good for micro- and macro-benchmarking, quick to set up, and relatively easy to use. 
 
## Summary of command to build filebench.
 
 Way to build filebench from officail site
 
 Because [filebench's repository](https://github.com/filebench/filebench) doesn't have configure file. 
 
 You have to generate the configure file. 
 
 filebench repository has dependency on libtoolize and automake tools to generate Makefile.in and configure files. 
 
```
Step 1. Generating autotill scripts

$ libtoolize
$ aclocal
$ autoheader
$ automake --add-missing
$ autoconf


Step 2 compilation and installation
$ ./configure
$ make
$ sudo make install
```
 
 After installation of filebench. 
 
 If you enter "$ filebench" in shell prompt, you can get result below.

```
$ filebench
Usage error: No runtime options specified

Usage: filebench {-f <wmlscript> | -h | -c [cvartype]}

  Filebench version 1.5-alpha3

  Filebench is a file system and storage benchmark that interprets a script
  written in its Workload Model Language (WML), and procees to generate the
  specified workload. Refer to the README for more details.

  Visit github.com/filebench/filebench for WML definition and tutorials.

Options:
   -f <wmlscript> generate workload from the specified file
   -h             display this help message
   -c             display supported cvar types
   -c [cvartype]  display options of the specific cvar type
```
---

this version is another way. But I don't recommend you the following version to build and compile filebench. 

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
--- 
 
 ## Reference
 
  - [filebench git repository](https://github.com/filebench/filebench)
 
  - [Way to build filebench](https://github.com/filebench/filebench/wiki)
 
  - [Way to compile filebench](https://github.com/zfsonlinux/filebench)
