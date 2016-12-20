---
layout: post
title: /dev Directory
subtitle: Whta is /dev Directory ?
category: Linux
tags: [linux, concept]
permalink: /2016/03/28/Dev_Directory/
---

this refers to <a href = "http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/dev.html"> dev of Linux File system Hierarchy</a>

/dev is the location of special or device files. it is a very interesting directory that highlights one important aspect of Linux filesystem - everything is a file or directory. Look through this directory and you shoud hopefully see hda1, hda2 etc... which represent the various partitions on the first master drive of the system. /dev/cdrom and /dev/fd0 represent your CD-Rom drive and your floppy drive. this may seem strange but it will make sense if you compare the characterstics of files to that your hardware. Both can  be read from and written to. Take /dev/dsp, for instance. This file represents your speaker device. Any data written to this file will be re-directed to your speaker. if you try 'cat /boot/vmlinuz >/dev/dsp'(on a properly configured system) you should hear som sound on the speaker. That's the sound of your kernel! A file sent to /dev/lp0 gets printed. Sending data to and reading from /dev/ttyS0 will allow you to communicate with a device attached there - for instance, your modem.

The majority of devices are either block or character devices; however other types of devices exist and can be created. In general, 'block devices' are devices that store or hold data, 'character devices' can be thought of as devices that transmit or transfer data. For example, diskette drives, hard drives and CD-ROM drives are all block devices while serial ports, mice and parallel printer ports are all character devices. There is a naming scheme of sorts but in the vast majority of cases these are completely illogical.


```shell
total 724
lrwxrwxrwx    1 root     root           13 Sep 28 18:06 MAKEDEV -> /sbin/MAKEDEV
crw-rw----    1 root     audio     14,  14 Oct  7 16:26 admmidi0
crw-rw----    1 root     audio     14,  30 Oct  7 16:26 admmidi1
lrwxrwxrwx    1 root     root           11 Oct  7 16:26 amidi -> /dev/amidi0
crw-rw----    1 root     audio     14,  13 Oct  7 16:26 amidi0
crw-rw----    1 root     audio     14,  29 Oct  7 16:26 amidi1
crw-rw----    1 root     audio     14,  11 Oct  7 16:26 amixer0
crw-rw----    1 root     audio     14,  27 Oct  7 16:26 amixer1
drwxr-xr-x    2 root     root         4096 Sep 28 18:05 ataraid
lrwxrwxrwx    1 root     root           11 Oct  7 16:26 audio -> /dev/audio0
crw-rw----    1 root     audio     14,   4 Oct  7 16:26 audio0
crw-rw----    1 root     audio     14,  20 Oct  7 16:26 audio1
crw-rw----    1 root     audio     14,   7 Mar 15  2002 audioctl
lrwxrwxrwx    1 root     root            9 Oct 14 22:51 cdrom -> /dev/scd1
lrwxrwxrwx    1 root     root            9 Oct 14 22:52 cdrom1 -> /dev/scd0
crw-------    1 root     tty        5,   1 Jan 19 20:47 console
lrwxrwxrwx    1 root     root           11 Sep 28 18:06 core -> /proc/kcore
crw-rw----    1 root     audio     14,  10 Oct  7 16:26 dmfm0
crw-rw----    1 root     audio     14,  26 Oct  7 16:26 dmfm1
crw-rw----    1 root     audio     14,   9 Oct  7 16:26 dmmidi0
crw-rw----    1 root     audio     14,  25 Oct  7 16:26 dmmidi1
lrwxrwxrwx    1 root     root            9 Oct  7 16:26 dsp -> /dev/dsp0
crw-rw----    1 root     audio     14,   3 Oct  7 16:26 dsp0
crw-rw----    1 root     audio     14,  19 Oct  7 16:26 dsp1
crw--w----    1 root     video     29,   0 Mar 15  2002 fb0
crw--w----    1 root     video     29,   1 Mar 15  2002 fb0autodetect
crw--w----    1 root     video     29,   0 Mar 15  2002 fb0current
crw--w----    1 root     video     29,  32 Mar 15  2002 fb1
crw--w----    1 root     video     29,  33 Mar 15  2002 fb1autodetect
crw--w----    1 root     video     29,  32 Mar 15  2002 fb1current
lrwxrwxrwx    1 root     root           13 Sep 28 18:05 fd -> /proc/self/fd
brw-rw----    1 root     floppy     2,   0 Mar 15  2002 fd0
brw-rw----    1 root     floppy     2,   1 Mar 15  2002 fd1
crw--w--w-    1 root     root       1,   7 Sep 28 18:06 full
......
```

그리고 이번에 프로젝트를 하면서 알게 된 것이 있는데 

lsblk는 kernel에서 block device라고 생각하는 것들의 목록을 보여준다. 

그리고 /dev는 각종 drive를 보여준다. 

내가 커널 컴파일하고 최신 오픈소스를 이용하여 pci 기반의 SSD인식을 할때 가장 

삽질을 한 것중 하나가 /dev/nvme0라고 nvme로 장치를 인식에서 device는 잡혔는데 

왜 open channel SSD를 built in 해서 컴파이를 하고 나니 lsblk로 검색이 안된다는 것이다. 

이거는 어쩌면 당연한 것다. lihgnvm으로 저 PCI 기반으로 device를 block device로 인식을 

시켜야 하는데 안했으니 ㅜㅜㅜ 이 작업을 위해 ioctl이 있겄만 ....... 

이것을 모르고 고생으로 1주에서 2주정도를 자꾸 커널 컴파일에서 커널 소스 디버깅으로 

커널의 컴파일 세팅 menuconfig로 시간만 잡아 먹었다. ㅜㅜㅜㅜ 젠장 

아 그리고 identify 라는 커널의 함수는 host 가 장치에 신호를 보내 제대로 작동을 

하는지 작업을 하는 것이다. 
