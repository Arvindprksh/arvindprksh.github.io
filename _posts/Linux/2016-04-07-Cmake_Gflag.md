---
layout: post
title: Cmake and Gflag
subtitle: What is the Cmake and Gflag ?
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

# Command-Line Flags 

this refers to <a href  = "https://gobyexample.com/command-line-flags">gobyexample site.</a>

Command-line flags are a common way to specify options for command-line programs. For example, in wc -l the -l is a command-line flag.

if you know more about command-line option, please go to <a href = "http://www.catb.org/esr/writings/taoup/html/ch10s05.html">catb</a>

# gflags

this refers to <a href ="https://gflags.github.io/gflags/">gflags</a>

this is library that hadles commandline flags processing. In other words, gflags is the commandline flags library used within Google. it differs from othe library, such as getop(), in that flag definitions can be scattered around the source code, and not listed in one place such as main(). In practice, this means that a single source-code file will define and use flags that 
are meaningful to that file. Any application that link in that file will get the flags, and the gflags library will automatically handle that flag appropriately.

there's significat gain in flexibility, and ease of code reuse, due to this technique, However, there is a danger that two files will define the same flag, and then give an error when they're linked together.

now, Download and installation 

The gflags library can be downloaded from <a href = "https://github.com/gflags/gflags">Github.</a>

in command line, you use the command :

  git  clone  https://github.com/gflags/gflags.git
  
build and installation instruction is used with Cmake. 

this build system of gflags is since version 2.1 based on Cmake. 

```
the processes are  :

    1. Extract source files (for example, if you get release verison)
    2. Create build directory and change to it
    3. Run CMake to configure the build tool.
    4. Build the software using selected build tool
    5. Test the built software. 
    6. Install the built files
```

but On Unix-like system with GNU Make as build tool, these steps can be summarized by the following sequence of commands executed in a shell(e.g. bash), where $package and $version are shell variable which represent the name of this package and the obtained version of the software.

```shell
    $ tar -xzf gflags-$version-source.tar.gz
    $ cd gflags-$version
    $ mkdir build && cd build
    $ ccmake ..
        - Press 'c' to configur the build system and 'e' to ignore warnings.
        - Set CMAK_INSTALL_PREFIX and other CMake variables and options.
        - Continue pressing 'c' until the option 'g' is available.
        - Then press 'g' to generate the configuration files for GNU Make.
    $ make 
    $ make test (optional)
    $ make install (optional)
```

if you know more about the process above, refer to <a href ="https://github.com/gflags/gflags/blob/master/INSTALL.md">gflag's Install</a> 
  
when I ran a db_bench executable of rocksDB using the gflags above, error happened, 

the error was :

```shell
[hyunyoung.lee@localhost gflags]$ cd build/
[hyunyoung.lee@localhost build]$ ccmake ..

[hyunyoung.lee@localhost build]$ make
[ 16%] Building CXX object CMakeFiles/gflags_nothreads_shared.dir/src/gflags.cc.o
[ 33%] Building CXX object CMakeFiles/gflags_nothreads_shared.dir/src/gflags_reporting.cc.o
[ 50%] Building CXX object CMakeFiles/gflags_nothreads_shared.dir/src/gflags_completions.cc.o
Linking CXX shared library lib/libgflags_nothreads.so
[ 50%] Built target gflags_nothreads_shared
[ 66%] Building CXX object CMakeFiles/gflags_shared.dir/src/gflags.cc.o
[ 83%] Building CXX object CMakeFiles/gflags_shared.dir/src/gflags_reporting.cc.o
[100%] Building CXX object CMakeFiles/gflags_shared.dir/src/gflags_completions.cc.o
Linking CXX shared library lib/libgflags.so
[100%] Built target gflags_shared
[hyunyoung.lee@localhost build]$ make install
[ 50%] Built target gflags_nothreads_shared
[100%] Built target gflags_shared
Install the project...
-- Install configuration: "Release"
-- Installing: /usr/local/lib/libgflags.so.2.2.0
CMake Error at cmake_install.cmake:48 (file):
  file INSTALL cannot copy file
  "/home/hyunyoung.lee/gflags/build/lib/libgflags.so.2.2.0" to
  "/usr/local/lib/libgflags.so.2.2.0".

make: *** [install] Error 1
[hyunyoung.lee@localhost build]$ sudo make install
[sudo] password for hyunyoung.lee: 
[ 50%] Built target gflags_nothreads_shared
[100%] Built target gflags_shared
Install the project...
-- Install configuration: "Release"
-- Installing: /usr/local/lib/libgflags.so.2.2.0
-- Up-to-date: /usr/local/lib/libgflags.so.2.2
-- Up-to-date: /usr/local/lib/libgflags.so
-- Installing: /usr/local/lib/libgflags_nothreads.so.2.2.0
-- Up-to-date: /usr/local/lib/libgflags_nothreads.so.2.2
-- Up-to-date: /usr/local/lib/libgflags_nothreads.so
-- Up-to-date: /usr/local/include/gflags/gflags.h
-- Up-to-date: /usr/local/include/gflags/gflags_declare.h
-- Up-to-date: /usr/local/include/gflags/gflags_completions.h
-- Up-to-date: /usr/local/include/gflags/gflags_gflags.h
-- Up-to-date: /usr/local/lib/cmake/gflags/gflags-config.cmake
-- Up-to-date: /usr/local/lib/cmake/gflags/gflags-config-version.cmake
-- Up-to-date: /usr/local/lib/cmake/gflags/gflags-targets.cmake
-- Installing: /usr/local/lib/cmake/gflags/gflags-targets-release.cmake
-- Up-to-date: /usr/local/bin/gflags_completions.sh
[hyunyoung.lee@localhost build]$ cd /usr/local/lib
[hyunyoung.lee@localhost lib]$ ls
cmake  libgflags_nothreads.so  libgflags_nothreads.so.2.2  libgflags_nothreads.so.2.2.0  libgflags.so  libgflags.so.2.2  libgflags.so.2.2.0  pkgconfig
```

# CMake 

this article refers to <a href = "https://cmake.org/">CMake</a>

Build, Test and Package Your software With Cmake.

CMake is an open-source, cross-platform family of tools designed to build, test and package software. 

CMake is used to control the software compliation process using simple paltform and complier independent configuration files, and generate native makefile and workspaces that cna be used in the compiler environment of your choice.

the above content is CMake's brief instruction.

now, because build system of gflags is since version 2.1 based on CMake, I needed this tool for making flags library, .so file, but on centos 7.2, the latest version of cmake was Package cmake-2.8.11-5.el7.x86_64. so I installed cmake-.3.0.0 manually.

the process refers to <a href = "https://xinyustudio.wordpress.com/2014/06/18/how-to-install-cmake-3-0-on-centos-6-centos-7/">xinyustudio</a>

as for the way, the following is :

```
    1. Dwonloade <a href ="https://www.cmake.org/files/v3.0/cmake-3.0.0.tar.gz">cmake-3.0.0.tar.gz</a>
    2. tar -zxvf cmake-3.0.0.tar.gz
    3. cd cmake-3.0.0.tar.gz
    4. ./bootstrap
    5. gmake
    6. sudo gmake install
    7. after cd .. , sudo mv cmake-3.0.0 /usr/local/
    8. "gedit" or "vim" ~/.bashrc, In other words, fix .bashrc
      - PATH =/usr/local/cmake-3.0.0/bin:$PAHT
      - export PATH
    9. cd /usr/local/camke-3.0.0
    10. mkdir share
    11. cp -R /usr/local/share/cmake-3.0/ share/
    13. finally, check the version using "cmake --version" command.
```
