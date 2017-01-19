---
layout: post
title: New Command Of LINUX
subtitle: Command about SSD 
category: SSD (Solid State Drives)
tags: [summary]
permalink: /2017/01/11/New_Command_In_LINUX/
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---

## stty
   
  this command is for data transfer like etera term, 
  
  In other words, IF you read information of device using usb cable. You need to set port. 
  
  At that time. You probable need this command. 
  
  you can see simple example on [stackoverflow](http://stackoverflow.com/questions/9092791/set-stty-parameters)
  
  **You want to have a conversatin with Device using USB cable serial communication, I recommand this command you.**
  
```shell
stty -F $(/dev/tty or /dev/ttyUSB) 38400 line 0 min 1 time 5 ignbrk -brkint -icrnl -imaxbel \
        -opost -onlcr -isig -icanon -iexten -echo -echoe -echok -echoctl \
        -echoke
```

  let's see the code under some situation. 
  
### Option  
  
(-F, --file=DEVICE) : Open and use the specified DEVICE instead of stdin. 

### Special settings

(38400(N) ) : Set the input and output speeds to N [bauds](http://www.computerhope.com/jargon/b/baud.htm) (baud in tera term)

(line 0(N) ) : use line discipline N

(min 1(N) ) : with **-icanon**, set N charaters minimum for a completed read

(time 5(N) ) : with **-icanon**, set read timeout of N tenths a second

### Input settings

(ignbrk) : ignore break chararters. 

(-brkint) : breaks cause an interrupts signal. 

(-incrnl) : translate  carriage return to newline.

(-imaxbel) : beep and do not flush a full input buffer on a character. 

### Output Settings

(-opost) :  postprocess output

(-onlcr) : translate newline to carriage return-newline.

### local Setting

(-isig) : enable interrupt, quit, and suspend special charaters. 

(-icanon) : enable erase, kill, werase, and rprnt specail charaters. 

(-iexten) : enable non-Posix special characters

(-echo) : echo input charaters. 

(-echoe) : same as [-]crterase

(-ehcok) : echo a newline after a kill charater

(-echoctl) : same as [-]ctlecho

(-echoke) : same as [-]crterase


So simply, let's put you into situation when you try to get log with the above option. 

```shell
cat $(/dev/tty or /dev/ttyUSB) | \
while IFS= read -r line
do
    // put time or something before putting log
done > log file variable
```
 
 as you can see the above, later on I have to figure out  **IFS = read -r line**

```shel
$ echo $line
              --> blank line
```

if you want to print time 

```shell
time=$(date +"%Y-%m-%d %H:%M:%S.%N")
"[${time:0:$((${#time}-6))}]"
```

# [tr](http://www.computerhope.com/unix/utr.htm) 

  the **tr** command automatically translates(subtitutes, or maps) one set of characters to another. 

  if you want a example, see [this site](https://en.wikipedia.org/wiki/Tr_%28Unix%29)
  
  let's see the simple example.
  
  and The d flag causes tr to delete all tokens of the specified set of characters from its input, in this case, only a singly caracter set argument is used. the following command removes carriage return charaters like this :
    
```
tr -d '\r'
```
  on [stackoverflow](http://stackoverflow.com/questions/12747722/what-is-the-difference-between-a-line-feed-and-a-carriage-return)
  
  What is the carriag return.
  
  A line feed means moving one line forward. The code is \n. A carriage return means moving the cursor to the beginning of the line. The code is \r.

```shell
$(echo "$line" | tr -d '\r') # delete ^M, escape *
```

## lspci

  lspci command shows you what pci is conneted with server(computer)
  
### lspci -t
 
  lspci -t make some result of lspci to tree structure
  
  if you add -v option, the verbose option display detailed information about all devices. 
  
  lspci -vt
  
  additionally, if you want to cut tree. 
  
  lspci -t | cut -c110- 

  cut -c(column) option, from the entire tree.
 
``` shell
$ lspci -t | cut -c110- | more











+-04.0-[8a]--
+-08.0-[8b]--
+-0c.0-[8c]--
+-0d.0-[8d-af]----00.0-[8e-af]--+-01.0-[8f-95]----00.0-[90-95]--+-01.0-[91]----00.0
|                               |                               +-02.0-[92]----00.0
|                               |                               +-08.0-[93]--

```
  
  BUT just if you want to cut column, you don't need to use the **| more** command 
  
  As you can see the above figure, If you want to remove the blank on the result. 
  
  do it like this. 
  
  lspci -t | cut -c110- | grep -v ^$

```shell
lspci -t | cut -c110- | grep -v ^$
+-04.0-[8a]--
+-08.0-[8b]--
+-0c.0-[8c]--
+-0d.0-[8d-af]----00.0-[8e-af]--+-01.0-[8f-95]----00.0-[90-95]--+-01.0-[91]----00.0
|                               |                               +-02.0-[92]----00.0
|                               |                               +-08.0-[93]--
|                               |                               +-09.0-[94]----00.0
|                               |                               \-0a.0-[95]----00.0
|                               +-04.0-[96]--
|                               +-08.0-[97-9d]----00.0-[98-9d]--+-01.0-[99]----00.0
|                               |                               +-02.0-[9a]----00.0
|                               |                               +-08.0-[9b]--
|                               |                               +-09.0-[9c]----00.0
|                               |                               \-0a.0-[9d]----00.0
|                               +-09.0-[9e-a4]----00.0-[9f-a4]--+-01.0-[a0]----00.0
|                               |                               +-02.0-[a1]----00.0
```
  
  -v ^$ means erasing the blank.
 
 **If the number of pci slot is wrong, OS couldn't be booted. I knew this fact through experience of skhynix memory solution intern life**
 
 in this situation, after booting, computer couldn't enter BIOS. 
 
 So I have to configure the number of PCI slot to boot computer. 
 
 
## ls -l /sys/block/nvme*

```shell
$ ls -l /sys/block/nvme*
lrwxrwxrwx. 1 root root 0 Jan 18 21:04 /sys/block/nvme0n1 -> ../devices/pci0000:00/0000:00:1c.4/0000:04:00.0/nvme/nvme0/nvme0n1

$ lspci -tv
-[0000:00]-+-00.0  .........
           ..........
           +-1c.0-[01]--
           +-1c.3-[02-03]----00.0-[03]--
           +-1c.4-[04]----00.0  Device 1c5c:2204
           .........
```
 
As you can see the above code. let's compare both of them.
 
../devices/pci0000:00/0000:00:1c.4/0000:**04**:00.0/nvme/nvme0/nvme0n1

-[0000:00]-+-00.0  .........
           ..........
           +-1c.0-[01]--
           +-1c.3-[02-03]----00.0-[03]--
           +-1c.4-[**04**]----00.0  Device 1c5c:2204
           ......... 
 
## lsusb 

## ls -v /dev/ttyUSB*

 
## window key + ↑

  this makes terminal window big like the entire window

##  window key + ↓

  this makes terminal window small like the orginal size. 
  
## [wc](http://www.tecmint.com/wc-command-examples/)

```
 $ wc [options] filenames.
```

  The wc(word count) command in Unix/Linux operating systems is used to find out number of newline count, 
  
  word count, byt and charaters count in a files specified by the file  arguments, The syntax of wc command as shown below
  
  wc -l : Prints the number of line in a file. ---> this is mostly used in my case. 
  
  wc -w : Prints the number of words in a file. 
  
  wc -c : Display the count of bytes in a file.
  
  wc -m : Prints the count fo characters from a file. 
  
  wc -L : Prints only the length of the longest line in a file. 
  
  in my case 
  
```shell
# lsusb | grep USB | wc -l
8
```

## ls -v 

  this command sorts the result of **ls** alphabetically. 
  
  **lssub** checks the number of the hub which is added to device(SSD-nvme)
  
```shell
# lsusb | grep USB 
```

## ps -ef | grep cat

  after issuing the command,"pkill cat". I have to check up which process is excuted. 
  
  So with the above command, I could find out one process executed in duplication like this.

```
$ ps -ef | grep cat
root      9491 26936  0 20:45 pts/2    00:00:00 grep --color=auto cat
root     26996 26982  0 20:13 pts/2    00:00:00 cat /dev/ttyUSB0
......
root     26996 26982  0 21:13 pts/2    00:00:00 cat /dev/ttyUSB0
```
## pkill cat

  I can learn this command when I was confused because on linux Centos7, I want to converse to nvme device with serial port(USB-UART PORT).
  
  But I could get right information. because I didn't know that two of the same processes worked. So I have to kill the former process that had converstaion with the nvme before. 
  
  So after that, 
  
  when I execute ths cat process to have a converstion with NVMe device in USB-UART. 
  
 1. at first, I  Kill cat that processed before. 
  
 2. after that, I execute the program again to have a conversation with NVMe devcie  
 
 In other words, I want to resolve the situation of checking process state executed in duplication with **ps -ef | grep cat**. 
 
```
$ pkill cat
```
 
## cat /proc/cmdline  

  proc include log and configuration file of kernel 
  
  /proc/cmdline is related to booting, cpu isolation, cpu affinity.
  
  if you want to make cpu isolation and use cpu affinity. you have to change this file because in here you can add some option into BOOT_IMAGE.
  
  the following is my Centos server's /proc/cmdline

```shell
# cat /proc/cmdline 
BOOT_IMAGE=/vmlinuz-4.7.4-1.el7.elrepo.x86_64 root=UUID=some-number ro crashkernel=auto rhgb quiet isolcpus=cpu-number,cpu-number nohz_full=cpu-number,cpu-number rcu_nocbs=cpu-number,cpu-number processor.max_cstate=1 idle=poll LANG=en_US.UTF-8
```
<!--
BOOT_IMAGE=/vmlinuz-4.7.4-1.el7.elrepo.x86_64 root=UUID=some-number ro crashkernel=auto rhgb quiet isolcpus=4-19,24-39 nohz_full=4-19,24-39 rcu_nocbs=4-19,24-39 processor.max_cstate=1 idle=poll LANG=en_US.UTF-8
-->


(cpu-number, cpu-number) of isolcpus, nohz_full and rcu_nocbs,"isolcpus=cpu-number,cpu-number(for example, isolcpus=4-10,24-30)", is symmetric. In other words. if cpu number is 4-10. each cpu is rommate with 24-30 like the following. 

(4,24), (5,25), (6,26), (7,27), (8,28), (9,29), (10,30) and so on. 

**this is my configuration, So if your device is different from mine. rommate of cpu could be different.**

## tail filename 

 this command makes the files open from the bottom of the last line. basically, the number of the line is 10.

### tail -f(option) filename
  
  if you add -f(option) on tail command, and then you can continuously get feedback from the file when the file continually generates text

## more

  this command makes you easy about openning the big file. since this command makes the file open properly to the size of your cmd line window. 
  
  and then, you can read texts line by line.


## grep 


## ag


## blkid

  this command I used is for checking which file system is on block device. 

```
$ sudo blkid
[sudo] password for hyunyoung.lee: 
/dev/sda1: UUID="some number" TYPE="xfs" 
/dev/sda2: UUID="some number" TYPE="LVM2_member" 
/dev/mapper/domain_name-root: UUID="some number" TYPE="xfs" 
/dev/mapper/domain_name-swap: UUID="some number" TYPE="swap" 
/dev/mapper/domain_name-home: UUID="some number" TYPE="xfs" 
/dev/nvme0n1: LABEL="F2FS" UUID="some number" TYPE="f2fs" 

```

## id 

```
$ id
uid=1000(hyunyoung.lee) gid=1000(hyunyoung.lee) groups=1000(hyunyoung.lee) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

## gnuplot 

  this tool makes png file with plot on LINUX , my case is centOS7

##


---  
  
# nvme-cli command 

## nvme format /dev/nvme0n1

 this command makes nvme intial state 
 
 if you use the above command, after that, I can see "Success formatting namespace"
 
```shell
$ nvme format /dev/nvme0n1
Success formatting namespace:1

if you want to format mutiple nvme device

for i in `seq 0 31`; do (nvme format /dev/nvme${i}n1 &); done

in here, (~~~ &), in other words, & means this command is  executed on backgroud simultaneously
```
  
## [nvme list](https://github.com/linux-nvme/nvme-cli/blob/master/Documentation/nvme-list.txt)

  I think this command is not default on LINUX, BUT If YOU install nvme-cli(open source tool), You can use it. 
 
```shell
  $ nvme list 
```

  and then you can check the list of nvme. 
  
  For example
  
``` 
  Node      SN      Model       Version     Nmaesapce       Usage     Format      FW Rev. 
  -----    -----    ------      -------     -----------     --------  ---------   ---------
```

  -- I think this is so simple, but If you change the open source, you can get much information. 
  
## [nvme smart-log /dev/nvme0n1](https://github.com/linux-nvme/nvme-cli#alpinelinux)

  When I have to calculate WAF, of course, You can use [teraterm](https://ttssh2.osdn.jp/index.html.en), that is you need window and usb cable. 
  
  But just if you have linux machine, it easy to use nvme-cli tool with the following command. 
  
```shell
  $ nvme smart-log /dev/nvme0n1  
```

  in my test on Centos 7
 
```
# in my nvme-cli folder

$ sudo ./nvme smart-log /dev/nvme0n1
Smart Log for NVME device:nvme0n1 namespace-id:00000000
critical_warning                    : 0
temperature                         : 0 C
available_spare                     : 0%
available_spare_threshold           : 0%
percentage_used                     : 0%
data_units_read                     : 0
data_units_written                  : 0
host_read_commands                  : 0
host_write_commands                 : 0
controller_busy_time                : 0
power_cycles                        : 0
power_on_hours                      : 00
unsafe_shutdowns                    : 0
media_errors                        : 0
num_err_log_entries                 : 0
Warning Temperature Time            : 0
Critical Composite Temperature Time : 0
Temperature Sensor 1                : 0 C
Temperature Sensor 2                : 0 C
Temperature Sensor 3                : 0 C
Temperature Sensor 4                : 0 C
Temperature Sensor 5                : 0 C
Temperature Sensor 6                : 0 C
```

  as I can say, it is easy to get the result rather than tera term
  
  in tera term 
  
```
  smartdbg 0(option number)
```
  
  this is too much cost
  
 ### More extensible case with grep on smart-log
 
  In other words, see [his site](http://unix.stackexchange.com/questions/37313/how-do-i-grep-for-multiple-patterns)
 
 ```shell 
 $ sudo ./nvme smart-log /dev/nvme0n1 | grep 'data_units_written\|host_write_commands'
data_units_written                  : 0
host_write_commands                 : 0 
 ```
 
  
