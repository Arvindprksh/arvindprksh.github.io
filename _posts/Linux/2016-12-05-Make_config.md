---
layout: post
title: Difference between Make oldconfig and olddefconfig
subtitle: What is the Difference between Make oldconfig and olddefconfig ?
category: Linux
tags: [fio, compile]
permalink: /2016/12/05/Make_config/
---

# [Linux Kernel document of kconfig](https://kernel.org/doc/Documentation/kbuild/kconfig.txt)

 I will quote the above file for resolving my questaion of kernel build. 
 
 Use "make help" to list all of the possible configuration targets. 
 
## General 

 New Kernel release often introduce new config symbols. often more important, new kernel releases may rename configure symbols. when this happen, using a previously working .config file and running "make oldconfig" won't necessarily produce a working new kernel for you, so you may find that You may find that you need to see what NEW kernel symbols have been introduced. 
 
 To see a list of new config symbols when using "make oldconfig". use 
 
    cp user/somewhere/old.config  .config
    make listnewconfig
    
 and the config program will list any new symbols, one per line. 
 
    scripts/diffconfig .config.old .config | less. 
    
**After reading the above article, I suppose if I find error, I need to find any new symbol on "make *config" command**


# my example with openchannelSSD

After reading [Stackoverflow](http://stackoverflow.com/questions/4178526/what-does-make-oldconfig-do-exactly-in-the-linux-kernel-makefile) about .config. 

I have question about "make *config". 

I just wanted to test it, so I will test it as follows.  

this test is for verifying my thougt. 

my test is implemented on qemu-nvme for OpenChannelSSD with CentOS 7

The following is the same process before procedure below.

as a result, "make oldconfig" is the same from "make olddefconfig".

**but** when you type "make oldconfig", if you reply by default against oldconfig.

replying by default is easy, for example

in the case below of [Y/n/?], you just reply "y" to fit upper case. 

```shell
Use a virtually-mapped stack (VMAP_STACK) [Y/n/?] (NEW) Y
```

```shell
- preparing for kernel compile. 
$ su
Password:
# chmod u+w /etc/sudoers
# vim /etc/sudoers
- in /etc/sudoers, I registerd user
# chmod u-w /etc/sudoers
# exit
$ reboot
 
$ sudo yum groupinstall "Development Tools"
$ sudo yum install -y openssl-devel
$ sudo yum install -y ncurese-devel
$ sudo yum install -y qt-devel

- zsh & theme
$ sudo yum install zsh
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
$ vim ~/.zshrc

- kernel Download
$ git clone https://github.com/OpenChannelSSD/linux.git
$ cd linux
$ cp /usr/src/kernels/3.10.0-327.36.1.el7.x86_64/.config ./.config
```

- only make menuconfig

```shell 
# preparing for kernel compile
$ make help 
...
Configuration targets:
...
  menuconfig	  - Update current config utilising a menu based program
...
$ make menuconfig
```

- make oldconfig and make menuconfig 

```shell 
# preparing for kernel compile
$ make help 
...
Configuration targets:
  ...
  oldconfig	  - Update current config utilising a provided .config as base
...
$ make oldconfig
...
for example, queistion of configuration is like first letter.
  Use a virtually-mapped stack (VMAP_STACK) [Y/n/?] (NEW) Y
...
$ make menuconfig
```

- make olddefconfig and make menuconfig.
 
```shell 
# preparing for kernel compile
$ make help 
...
Configuration targets:
  ...
  olddefconfig	  - Same as silentoldconfig but sets new symbols to their
                    default value
...
$ make olddefconfig 
...
  HOSTCC  scripts/basic/fixdep
  HOSTCC  scripts/kconfig/conf.o
  SHIPPED scripts/kconfig/zconf.tab.c
  SHIPPED scripts/kconfig/zconf.lex.c
  SHIPPED scripts/kconfig/zconf.hash.c
  HOSTCC  scripts/kconfig/zconf.tab.o
  HOSTLD  scripts/kconfig/conf
scripts/kconfig/conf  --olddefconfig Kconfig
#
# configuration written to .config
#
...
$ make menuconfig
```
 
**after "make menuconfig"**

pblk.20 on OpenchannelSSD


![](/img/Image/Linux/2016-12-05-Make_config/Source_install_OpenchannelSSD_(pblk20).png)

like [officail site's source install](http://openchannelssd.readthedocs.io/en/latest/gettingstarted/#source-install). 

![](/img/Image/Linux/2016-12-05-Make_config/make_menuconfig_pblk_20_OpenchannelSSD.png)

![](/img/Image/Linux/2016-12-05-Make_config/Make_menuconfig(pblk20)-NVM_Express_block_device.png)


```shell 
$ sudo make modules_install
$ sudo make install
```

The result of rebooting is as follows. 

![](/img/Image/Linux/2016-12-05-Make_config/Booting_success_of_the_new_linux.png)


# on the above setting, Another experiment, 

on Host OS

```
-making ramdisk 
$ mkdir ./root/ramdisk
$ sudo mount -t tmpfs -o size=2G tempfs ./root/ramdisk

- making virtual disk 
$ dd if=/dev/zero of=~/root/ramdisk/blknvm bs=1G count=4

- qemu-nvme install
$ git clone https://github.com/OpenchannelSSD/qemu-nvme.git
$ cd qemu-nvme
$ ./configure --python=/usr/bin/python2 --enable-kvm --target-list=x86_64-softmmu --enable-linux-aio --prefix=$HOME/qemu-nvme

-maybe error happen.
$ sudo yum install -y gtk2-devel
$ sudo yum install libaio-devel

$ make -j8
$ sudo make install
```

on Geuste OS

```shell

-install lnvm 
$ git clone https://github.com/OpenChannelSSD/lnvm.git
$ cd lnvm
$ make
$ sudo make install

- install fio

$ git clone http://git.kernel.dk/fio.git
$ cd fio
- zlib-devel or libaio-devel
$ sudo yum install zlib-devel  or $ sudo yum install libaio-devel
$ ./configure
$ make
$ sudo make install
$ fio -version

- shell script of fio 

# !/bin/zsh

BS=4k(lower case)
RW=randwrite

for RDN in $(seq 0 9) 
do

fio --name=$BS-$RW-$RDN \
 --filename=/dev/hyun \
 --rw=$RW \
 --bs=$BS \
 --ioengine=libaio \
 --numjobs=1 \
 --iodepth=256 \
 --direct=1 \
 --thread \
 --write_iops_log=$BS-$RW-$RDN \
 --log_avg_msec=1000 \
done
```

# Reference 

 [Linux kernel Document's Kconfig](https://kernel.org/doc/Documentation/kbuild/kconfig.txt)
 
 [Stackover flow's make oldfonfig](http://stackoverflow.com/questions/4178526/what-does-make-oldconfig-do-exactly-in-the-linux-kernel-makefile)
 
 [installing way of kernel of stackExchange](http://unix.stackexchange.com/questions/42144/modules-not-found-error-during-kernel-install)
 
 [forum of Gentoo](https://forums.gentoo.org/viewtopic-t-827203-highlight-menuconfig.html)
