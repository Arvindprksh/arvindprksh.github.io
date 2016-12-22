---
layout: post
title: options for OpenChannelSSD and LightNVM on QEMU-NVMe
subtitle: What options is in QEMU-NVMe for OpenChnnelSSD and LightNVM ? 
category: SSD (Solid State Drives)
tags: [lightnvm, qemu, nvme]
permalink: /2016/10/27/Options_For_OpenChannelSSD_On_QEMU_NVMe/
---

[the original qemu-nvme github](https://github.com/nvmeqemu/nvmeqemu) & [the qemu-nvme github for OpenchannelSSD](https://github.com/OpenChannelSSD/qemu-nvme)

# Usage Of QEMU

Basically, If you want to know qemu emulator option, just recommend [Qemu weilnetz](http://qemu.weilnetz.de/qemu-doc.html#pcsys_005fintroduction) in [official QEMU site](http://wiki.qemu.org/Documentation)

> qemu-system-x86_64 -m 1024 -hda PATH -device nvme -smp 1 --enable-kvm -device 

  - smp [cpu=]n [,.....]
  
    - This meaning is that **you simulate the SMP system with n CPUs**, And another missing options will be computed.
    
    - If you want to know about SMP(symmetric multiprocessing), [This wikipedia](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) is good to you
    
  - m [size=]megs [,....]
  
    - **Sets guest startup RAM size to megs megabytes**, Default is 128 MiB, Optionally, you can use suffix of "G", "M" that signify gigabytes and megabytes repectively

  - device driver [,...]
  
    - **Add device driver**, 
    
  - drive option[,...]
  
    Define a new drive. Valid options are:
  
    - option : file=file
    
      - this option defines which disk image to use with this drive
   
   - enable-kvm 
   
    - **Enable KVM full virtualization support**. this option is only available if KVM support is enabled when compiling
    
    - this case is much better performance, Because of virtualization. i.e using hardware feature.
    
# [Usage of QEMU-NVMe with OpenchannelSSD](https://github.com/OpenChannelSSD/qemu-nvme/blob/master/hw/block/nvme.c). 

<!--
sudo ~/qemu-nvm/bin/qemu-system-x86_64 -m 1G -smp 1 --enable-kvm -hda /var/lib/libvirt/images/cents7.0.qcow2 -drive file=~/root/ramdisk/blknvm,if=none,id=mynvme, -device nvme,drive=mynmve,serial=deadbeef,lver=1,ll2pmode=0,ldebug=1 -monitor stdio
-->

```
-drive file=<file>, if=none,id=<drive_id>  
-device nvme,drive=<drive_id>,serial=<serial>,id=<id[optional]>mat
```

> drive file=/home//blk_nvme_device,if=none,id=lightnvme -device nvme,drive=lightnvme,serial=deadbeef,lver=1,lba_index=3,nlbaf=5,lchannels=1,namespaces=1

```c
  - namespace=<int> : Namespaces to make out of the backing storage, **Defualt:1**
  
  - lver=<int> : version of the LightNVM standard to use, **Default:1**
  
  - ll2pmode=<int> : LightNVM op. mode. 1: hybrid, 0: full host-based. **Default:1**
  
  - lmtype=<int> : media type. Default: 0 (Nand Flash Memory) **Default:0**
  
  - lsec_size=<int> : Controller Sector Size. **Default:4096**
  
  - lsecs_per_pg=<int> : Number of sectors in a flash page. **Default:1**  
  
  - lpgs_per_blk=<int> : Number of pages per flash block. **Default:265**  
  
  - lmax_sec_per_rq=<int> : Maximum number of sectors per I/O request. **Default:64**
  
  - lfmtype=<int> : Flash media type. **Default : 0 (SLC)**
  
  - lnum_ch=<int> : Number of controller Channels. **Default:1**
  
  - lnum_lun=<int> : Number of LUNs per Channels, **Default:1**  

  - lum_pln=<int> : Number of flash Planes per LUN. Supported sigle (1). 

  - lreadl2ptbl=<int> : Load logical to physical table. 1: yes, 0: no. **Default: 1** 
  
  - ldebug : Eanble LightNVM debugging. **Default: 0 (disable)**
  
  #######
  - nlbaf=<int> : Number of logical block formats, **Default:1** 
  
  - lba_index=<int> : Default namespace block format index, **Default:0** 
  
  - mdts=<int> : Maximum data transfer size, **Default:5**
```

<!--
 Back end file 4GB
```c 
  - namespace=<int> : Namespaces to make out of the backing storage, **Defualt:1**
  
  - lver=<int> : version of the LightNVM standard to use, **Default:1**
  
  - ll2pmode=<int> : LightNVM op. mode. 1: hybrid, 0: full host-based. **Default:1**
  
  - lmtype=<int> : media type. Default: 0 (Nand Flash Memory) **Default:0**
  
  - lsec_size=<int> : Controller Sector Size. **Default:4096**
  
  - lsecs_per_pg=<int> : Number of sectors in a flash page. **Default:1**  maybe : increase 4
  
  - lpgs_per_blk=<int> : Number of pages per flash block. **Default:265**  maybe : increase 512
  
  - lmax_sec_per_rq=<int> : Maximum number of sectors per I/O request. **Default:64**
  
  - lfmtype=<int> : Flash media type. **Default : 0 (SLC)**
  
  - lnum_ch=<int> : Number of controller Channels. **Default:1**
  
  - lnum_lun=<int> : Number of LUNs per Channels, **Default:1**  maybe : increase to 4

  - lum_pln=<int> : Number of flash Planes per LUN. Supported single (1).  maybe : increase to 2

  - lreadl2ptbl=<int> : Load logical to physical table. 1: yes, 0: no. **Default: 1** 
  
  - ldebug : Eanble LightNVM debugging. **Default: 0 (disable)**
  
--- the following is specific component for lightNVM
  - nlbaf=<int> : Number of logical block formats, **Default:1**  maybe : increase to 5 
  
  - lba_index=<int> : Default namespace block format index, **Default:0**  maybe : increase to 3
  
  - mdts=<int> : Maximum data transfer size, **Default:5** maybe : increase to 10, 
```
-->

  1. With above options, nand device's feature. 
  
  > lightNVM operation mode : ll2pmode manages, So 1: hybrid, 0: full host-based mode 
  
  |         |                   |
  |---------|-------------------|
  | channel | lun(plane only 1) |
  
  
  [Openchannel SSD basic NVMe Concept](https://github.com/OpenChannelSSD/qemu-nvme/blob/master/hw/block/nvme.c)
  
```c 
   /* We devide the address space linearly to be able to fit into the 4KB
  * sectors that the nvme driver divides the backend file. We do the
  * division in LUNS - BLOCKS - PAGES - SECTORS. If there is 2 or 4
  * planes, each LUN is unfolded into planes.
  *
  * For example a quad plane configuration is layed out as:
  * -----------------------------------------------------------
  * |               QUAD PLANE                |
  * -------------- -------------- -------------- --------------
  * | LUN 00 | | LUN 01 | | LUN 02 | | LUN 03 |   -----> die concept
  * -------------- -------------- -------------- --------------
  * | BLOCKS |           ...         | BLOCKS |
  * -------------
  * | PAGES  |            ...        | PAGES  |
  * -----------------------------------------------------------
  * |               ALL SECTORS               |
  * -----------------------------------------------------------
  */
```
 
  > type of nand : SLC , l2p table : you can always load.
  
  I/O units 
  
  > sector size of controller : 4KB   
  > number of sertors per a flash page : 1 , So a page = a sector = 4KB    
  > number of pages in a flash block : 256, So a block = 256 pages = 256 sectors = 1(256*4)MB    
  > Maximum number of sectors per I/O request : 64 , So I/O Unit<Write unit> = 64 sectors * 4KB = 256KB  
  
with above enviroment, I have to evaluate OpenChannelSSD. 


# Qemu-NVMe for OpenchannelSSD with pblk

1. How to Install
---

Basically, intalled method is the same. when you install **rrpc**. 

i.e, you need [QEMU-NVMe](https://github.com/OpenChannelSSD/qemu-nvme) for OpenChannel, [LNVM tool](https://github.com/OpenChannelSSD/qemu-nvme/), lastly, You need [linux version](https://github.com/OpenChannelSSD/linux) supporting **pblk**.

After you save the whole thing above, you can start **pblk**

For details, refer to manual of each sites 

Briefly about procedure of installing. 

  1. QEMU-NVMe
```shell
  $ git clone https://github.com/OpenChannelSSD/qemu-nvme.git
  $ cd qmeu-nvme
  $ ./configure --python=/usr/bin/python2 --enable-kvm --target-list=x86_64-softmmu --enable-linux-aio --prefix=$HOME/qemu-nvme
  $ make -j8
  $ make install
```
  
  2. LNVM On Centos 7 
  
  * If you have another version, unbuntu. Just refer to officail site. 
```shell
  $ git clone https://github.com/OpenChannelSSD/lnvm.git
  $ cd lnvm
  $ make 
  $ sudo make install
```
  
  3. procedure of registering rrpc
  
```shell
  $ lsblk -t // you can check whether QEMU-NVMe for openchannelSSD works or not. 
  $ sudo ./lnvm/lnvm devices
  $ sudo ./lnvm/lvnm info
  $ sudo ./lnvm/lnvm -d init nvme0n1 // after checking list of 'sudo ./lnvm/lnvm devices', you can put the result of devices in location of nvme0n1  
  $ sudo ./lnvm/lnvm -d create nvme0n1 -n hyun -o 0:3 
  // -d means device wiht media manager, -n means target name, -0 : target option, such as die. i.e numbers of luns.
  $ sudo ./lnvm/lnvm hyun // I've not used this command -> I wrote this command as the official site explain.
```
  
  4. Linux for OpenChannelSSD
  
```shell
  $ git colone https://github.com/OpenChannelSSD/linux.git
  $ cd linux
  * if you need it
  $ git checkout version_you_need
  from here, the rest is the same from compiling kernel
  $ cp ./correct_config_file ./linux/.config
  $ make menuconfig
  $ make 
  $ sudo make modules_install install
  $ reboot OR shutdown -r now
```

For procedure of registering pblk on QEMU-NVMe

  **I created virtual drive for nvme device.**

  > $ dd if=/dev/zero of=~/ramdisk/blknvme bs=1G count=4   

  >  start QEMU-NVMe for openchannel.    

  > $ sudo ~/qemu-nvme/bin/qemu-system-x86_64 -m 1G -smp 1 --enable-kvm -hda /var/libvirt/images/centos7.0.qcow2 -drive file=~/ramdisk/blknvme,if=none,id=mynvme -device nvme,drive=mynvme,serial=deadbeef,lver=1,ll2pmode=0,llum_pln=2,lsecs_per_pg=4,lpgs_per_blk=512,ldebug=1 -monitor stdio   
  
  In order to check whether QEMU-NVMe for OpenChannelSSD works or not  
  
  > $ lsblk -t      

  > register lightNVM with lnvm      
  
     Check if device for lightNVM is in your kernel. 
    
    > $ lnvm devices   
    > $ lnvm info   

 if Yes, put Generic Media Manager on your SSD with lnvm.  
    
    > $ lnvm init -d nvme0n1   
    
 If you want to othe media manager   
    
    > $ lnvm init -d nvme0n1 -m other   

  next, connect taget you want on state of 3-2 with lnvm 
    

  > $ lnvm create -d nvme0n1 -n hyun -t pblk (OR rrpc) (-o 0:3)    
    
  **IF rrpc** 
  
  > $ lsblk -t    
  
  after above. you can find block device named hyun.    
  
  > dmesg | grep 'nvm'    
  
  after abvoe. you can find the initial configuration. 
    
  **IF pblk**   
  
  > $ lsblk -t     
  
  > $ dmesg | grep 'pblk'    

  command for execution of QEMU-NVMe
   
  this base nvme in RAMDisk 
  
```shell  
  $ mkdir ./ramdisk 
  $ sudo mount -t tmpfs -o size=5G ./ramdisk
  $ dd if=/dev/zero of=~/ramdisk/blknvme bs=1G count=4
  $ sudo ~/qemu-nvme/bin/qemu-system-x86_64 -m 1G -smp 1 --enable-kvm -hda /var/libvirt/images/centos7.0.qcow2 -drive file=~/ramdisk/blknvme,if=none,id=mynvme -device nvme,drive=mynvme,serial=deadbeef,lver=1,ll2pmode=0,llum_pln=2,lsecs_per_pg=4,lpgs_per_blk=512,ldebug=1 -monitor stdio
```   

  ![](/img/Image/SSD-Solid_State_Drives/2016-10-27-Options_For_OpenChannelSSD_On_QEMU_NVMe/pblk 19 FIO TEST git.png)
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-10-27-Options_For_OpenChannelSSD_On_QEMU_NVMe/pblk 19 FIO Test git 2.png)
  
That is all, 

# What is differenc between rrpc and pblk.

 From now on, this article just is my analysis after reading specification of lihgtnvm and seeing the source code(kernel 4.4 version)

 NEW Specification of CLEX lean to pblk. but as of now(october 31, 2016), the kernel mainline from 4.4 to 4.8 only include rrpc
 
 * rrpc meaning is round robin page-based hybrid FTL. 
 
 * pblk - to filesystem, pblk appears like block device in lightNVM module.
 
 lightNVM's Hybrid mode is if set to 1, L2P MAP is in device. 
 
                           if set to 0, L2P MAP is in host.
                           
 as of now(october 31, 2016), CLex support of PPA is hybrid Page Address on rrpc. But it is not neccesary for OpenChannelSSD.
 
 So they claim that later on this disappears and folded inot Physical Page write. 
 
 I assume that rrpc is round robin page-based hybrid FTL. i.e feature of rrpc's physcal address is hybrid Page address. 
 
 anyway, this technology starts from 2015, and Now many things is changed. 
 
# kernel DEBUG 

## how to debug kernel

### the Simplest method

 - [Uing printk](http://elinux.org/Debugging_by_printing#Usage)

### [* important thing!](https://www.kernel.org/doc/Documentation/kbuild/makefiles.txt)

 - when you compile kernel, you can configure log level. 
 
   pr_debug (..) or printk(Debug option.....)
   
   if you compile normally, you can not get log of the above functions. 
   
   So you have to configure to see debug functions print. 
   
   there are two ways to do it. 
   
   1. [DDEBUG](https://www.kernel.org/doc/local/pr_debug.txt)
   
   - DDEBUG option
    
   > ccflags-y := -DDEBUG   
   
   > I quoted portion of [kernel' Makefile.txt](https://www.kernel.org/doc/Documentation/kbuild/makefiles.txt), as follows  

```
  --- 3.7 Compilation flags

    ccflags-y, asflags-y and ldflags-y
	These three flags apply only to the kbuild makefile in which they
	are assigned. They are used for all the normal cc, as and ld
	invocations happening during a recursive build.
	Note: Flags with the same behaviour were previously named:
	EXTRA_CFLAGS, EXTRA_AFLAGS and EXTRA_LDFLAGS.
	They are still supported but their usage is deprecated.

	ccflags-y specifies options for compiling with $(CC).

	Example:
		# drivers/acpi/Makefile
		ccflags-y := -Os
		ccflags-$(CONFIG_ACPI_DEBUG) += -DACPI_DEBUG_OUTPUT

	This variable is necessary because the top Makefile owns the
	variable $(KBUILD_CFLAGS) and uses it for compilation flags for the
	entire tree.

	asflags-y specifies options for assembling with $(AS).

	Example:
		#arch/sparc/kernel/Makefile
		asflags-y := -ansi

	ldflags-y specifies options for linking with $(LD).

	Example:
		#arch/cris/boot/compressed/Makefile
		ldflags-y += -T $(srctree)/$(src)/decompress_$(arch-y).lds

    subdir-ccflags-y, subdir-asflags-y
	The two flags listed above are similar to ccflags-y and asflags-y.
	The difference is that the subdir- variants have effect for the kbuild
	file where they are present and all subdirectories.
	Options specified using subdir-* are added to the commandline before
	the options specified using the non-subdir variants.

	Example:
		subdir-ccflags-y := -Werror

    CFLAGS_$@, AFLAGS_$@

	CFLAGS_$@ and AFLAGS_$@ only apply to commands in current
	kbuild makefile.

	$(CFLAGS_$@) specifies per-file options for $(CC).  The $@
	part has a literal value which specifies the file that it is for.

	Example:
		# drivers/scsi/Makefile
		CFLAGS_aha152x.o =   -DAHA152X_STAT -DAUTOCONF
		CFLAGS_gdth.o    = # -DDEBUG_GDTH=2 -D__SERIAL__ -D__COM2__ \
				     -DGDTH_STATISTICS

	These two lines specify compilation flags for aha152x.o and gdth.o.

	$(AFLAGS_$@) is a similar feature for source files in assembly
	languages.

	Example:
		# arch/arm/kernel/Makefile
		AFLAGS_head.o        := -DTEXT_OFFSET=$(TEXT_OFFSET)
		AFLAGS_crunch-bits.o := -Wa,-mcpu=ep9312
		AFLAGS_iwmmxt.o      := -Wa,-mcpu=iwmmxt


--- 3.9 Dependency tracking

	Kbuild tracks dependencies on the following:
	1) All prerequisite files (both *.c and *.h)
	2) CONFIG_ options used in all prerequisite files
	3) Command-line used to compile target

	Thus, if you change an option to $(CC) all affected files will
	be re-compiled.
```  

In addition, you need to know [dynamic debug](https://lwn.net/Articles/434856/) and [Debug file System](https://www.kernel.org/doc/Documentation/filesystems/debugfs.txt)
 
   2. [adjust loglevel](https://kernelnewbies.org/FAQ/LinuxKernelDebug101)
   
   - echo 8 > /proc/sys/kernel/printk

If you want to debug kernel, click [elinux.org](http://elinux.org/Debugging_by_printing#Log_Levels)

### Finally, To sum up about the above debug

1. with Makefile 

  > DDEBUG

<!-- ccflags-y := -DDEBUG -->


2. with loglevel
```shell
 $ cat /proc/sys/kernel/printk   
 4	4	1	7
 $ su
 # echo 8 > /proc/sys/kernel/printk
 # cat /proc/sys/kernel/printk
 8	4	1	7
```	

after change the loglevel , I cannot get details than compilation time. 

I mean, to check pr_debug, pr_err function, when i compile, I think i neet to fix Makefile.    

### [blktrace](http://wiki.dreamrunner.org/public_html/Low_Latency_Programming/blktrace.html) 

 - this just shows you trace of IO. 
 
 add "ccflags-y := -DDEBUG" in lingtNVM's Makefile.

### [target-specific Variable Values](http://stackoverflow.com/questions/1079832/how-can-i-configure-my-makefile-for-debug-and-release-builds)
