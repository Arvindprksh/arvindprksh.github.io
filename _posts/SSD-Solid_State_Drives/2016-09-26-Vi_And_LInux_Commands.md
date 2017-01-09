---
layout: post
title: Vi Command And Linux Command 2
subtitle: While I do opensource project, These command is What I learned.  
category: SSD (Solid State Drives)
tags: [vi, command]
permalink: /2016/09/26/Vi_And_LInux_Commands/
---

From now on, I will make a list of vi command for me, in addition, click [Computerhope's vim](http://www.computerhope.com/unix/vim.htm)

# Vim/vi command

# split 

  this command show you spliting window. So you can choose the two type. 
  
  one is vertical split. another is horizontal split. 
  
  [Microshell's Split Screen in vi](http://www.microshell.com/programming/quick-tips/split-screen-in-vi/) is related to split command
 
 
## Split screen horizontally 
 
  - :split   or :sp 
  
  > The above command will split vi screen horizontally. I can also supply an optional filename.
  

## Split screen vertically

  - :vsplit  or :vsp
  
  > The above command wiil split vi screen vertically. And this command will also take filename optionally. 
  
## How to navigate between screens

  - Navigating is pretty easy on vi. just type **ctrl+w ctrl+w** twice to jump between screens. 
  
  - Another way is using **ctl-w then arrow key(hjkl)** to move to different screens. 
  
  - so To move to the right, press 
  - Ctrl-w l
  
  - to left : Ctrl+w h
  
  - to up : Ctrl+w k
  
  - to down : Ctrl+w j
  
  For example. use  :e option, then move to another screen.  
  
## unsplit / close split-ed screens

  - navigate to the screen that you want to close/ unsplit, thene basically type **:q** to quit editing that screen.
  
## To resize split-ed screens. 

  - For horizontal split, navigainte to the screen you want to resize then type **ctrl-w then + or -** to increase or decrease horizontal size by 1. there are another way. For example 10 ctrl+w + will increase increase the window size by 10. 
  
  - For vertical split. navigate to the screen to resize then type **ctrl+w > or <** to increase or decrease vertical size by 1. There are anoteher way like the above.
  
  I want you to see [Vim wikia's Resize Splits more Quickly](http://vim.wikia.com/wiki/Resize_splits_more_quickly) to resize 

## How to cut and paste or copy and paste

  1. Basically, If you want make a block, Just press **v to begin chararter-based** or **V to selec whole lines** or **Ctrl+v to select a block**.
   
  2.If you know the above. First of all Position the cursor at the beginning of the text you want to cut / copy
  
  3. Move the cursor to the end of the text to be cut/copied. While selecting text, you can perform searches and other advanced movement. 
  
  4. Press **d(delete)** to cut, or **y(yank)** to copy. 
  
  5. Move the cursor to the desired paste location.
  
  6. Press **p** to paste after the cursor, or **P** to cursor before  
  
 If you want to change the selected text, press **c** instead of **d** or **y** in step 4. In a visual selection, pressing **c** performs a change by deleting the selected text and entering insert mode so you can type the new text
 
 for video of block, [Youtube's cut, paste, copy](https://www.youtube.com/watch?v=ar8Jls9rh64)
 
# Linux command 

## Tab command

  - **tabe .**
  
  > this command(tab) makes the new tab window.  
  > Just think about meaning of tab    
  > tabe . means in new tab, edit the current file or diretory(.)   
  
  if you want to move to other tab window. 
  
  just type **gt** 
  
  if You want to know navigation of tab. just visit [Vim wikea's Using Tab Pages](http://vim.wikia.com/wiki/Using_tab_pages)
  
  - Navigation 
  
  > :tabs          - list all tabs including their displayed windows.  
  > :tabm 0        - move current tab to first   
  > :tabm          - move current tab to last  
  > :tabm {i}      - move current tab to position i+1   
  >   
  > :tabn          - go to next tab. 
  > :tabp          - go to previous tab
  > :tabfirst      - go to first tab
  > :tablast       - go to last tab.
  
  in normal mode. you can type
  
  > gt             - go to next tab   
  > gT             - go to previous tab   
  > {i}gt          - go to tab to position + i    
  
  Note that the gt command counts form one. That means 3gt will jump to the third tab. Also notice is 0st and 1gt mean the same thing : jumping to the first tab.  
  
  in normal mode in insert mode. you can type
 
  > Ctrl-PgDn      go to next tab   
  > Ctrl-PgUp      go to previous tab    
  
  
## How to observe process state.

  - top
  
  - [htop](http://elearning.wsldp.com/pcmagazine/centos-install-htop/)
  
  the above program is useful to supervise the whole process state.
  
  - ps aux
  
  This command also shows you processes executed. 
  
## $? 

  - you can find out return value of last execution. 
  
## vimdiff 

  - you can compare tow files with vim/vi
 
## diff

  - you can compare two files
  
## xxd

  - you can see the document as hexa code

## [od](http://www.thegeekstuff.com/2012/08/od-command/)

  - od command make output of files different. 
 
  - If you want more details, click od title!

## history

  - You can see the past commands.
  
## chmod

   If you want to know , just visit [Computerhope uchmod](http://www.computerhope.com/unix/uchmod.htm)
   
   - chmod options permissions filename.
   
   - chmod 754 filename
   
   - chmod is used to change the permission of files or directories. 
   
   - in chmod 755 filename
   
   - 755 in permissions means user, group, other. 

   reae means 4
   
   write means 2
   
   execute means 1
  
   though I have no money, 
  
## Ctrl-r

 Uset the CTRL-R key to perform a "reserve-i-seachr", For example, If you wanted to use the command you used the last time you used snort, you would type : 
 
 **CTR-R** then type "snort". 
 
 What you will see in the console window is : 
 
 (reverse-i-search)' : 
 
 after you have typed what you are looking for, use the **Ctrl-R** key combination to scroll backward through the history.
 
 Use **CTR-R** repeatedly to find every reference to the string you've entered. Once you've found the command you're looking for. Use **[Enter]** tor execute it. 
 
 Alternatively, using the right or lefet arrow will place the commnad on an actual commandline so you can edit it. 
   
## history n 

 n is the number of command that You want to look for from last command.
 
 I recommend you [this Geekstuff's history](http://www.thegeekstuff.com/2008/08/15-examples-to-master-linux-command-line-history/)
 
 the site explanin to you example of usage of command line history. 
   
## scp 

  secure copy command with ssh(secure shell)
  
  [computerHope's scp](http://www.computerhope.com/unix/scp.htm)
  
  the following article refer to the above [computerHope's cco](http://www.computerhope.com/unix/scp.htm)
  
  this command has big difference from cp.
  
  that is  one or both of the locations are on a remote system. 
 
  For example, 
  
  cp /home/stacy/images/image*.jpg /home/stacy/archive
  
  similarly, you could use the scp command :
  
  scp /home/stacy/images/image*.jpg stacy@myhost.com:/home/stacy/archive
  
  stacy : user ID
  myhost.com  : server IP
  
  When You want to move to home directory. 
  
  in part of stacy@myhost.com:/home, you have to fix. 
  
  for more detail, click [this stackExchange](http://unix.stackexchange.com/questions/47909/transfer-files-using-scp-permission-denied)
  
  To sum up, if what you want to do is to transfer them to your home directory, You can substitute the path to your home directory with shortcur ~/. 
  
  The following shows you a successful example. 
 
```bash
  scp ./linux.tar.gz  hyunyoung.lee@IPv4 a
  ress:/home
  hyunyoung.lee(user_id)@IPv4 address's password: 
  scp: /home/linux.tar.gz: Permission denied
  
  after fixing. 
  
  scp ./linux.tar.gz  hyunyoung.lee@IPv4 address:~/
  hyunyoung.lee(user_id)@IPv4 address's password: 
  linux.tar.gz                                                                  100% 1228MB 153.5MB/s   00:08  
```
  
## lspci

 **lspci -vt**

 This command makes list of all PCI devices.
 
 I refered to [The Geekstuff's lspci](http://www.thegeekstuff.com/2014/04/lspci-examples)
 
 lspci stands for list pci. Think of this command as "ls" + "pci"
 
 This will display information about all the PCI bus in your server. 
 
 Apart from displaying information about the bus, it will also display information about all the hardware devices that are connected to your PCI and PCIe bus. 
 
 For example, It will display information about Ethernet cards, RAID controllers, Video cards, etc.
 
 lspci utility is part of the pciutils package.
 
 **If you want to print like Tree format**
 
 you have to use -t option 
 
 
 **Detailed Device information**
 
 you have to use -v option.
 
 For addtional level for berbosit, you can use -vv or -vvv.
  
 In my case : lspci -vt
 
 **later on, If I use the supported function, I need to use printk function, I can get information about vendor using pciutils.**
 
 If you want to know more details. I recommend [this site,The Geekstuff's lspci](http://www.thegeekstuff.com/2014/04/lspci-examples)
 
## lsblk

  **lsblk -t**

  block device list, in other words, The lsblk command allow you to display a list of availablve block devices. 
  
  for more details. please go to [redhat site](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-sysinfo-filesystems.html) 
  
  for your information, I attach **[Fibrevillage's lsblk](http://fibrevillage.com/storage/53-lsblk-command-examples)** explianing lsblk 
  
  And For [column in details,"Suteruser"](http://superuser.com/questions/778686/linux-lsblk-output), And [another one,"Linoxide".](http://linoxide.com/linux-command/linux-lsblk-command/) 
  
  lvm(logical volume manager)(https://en.wikipedia.org/wiki/Logical_Volume_Manager_%28Linux%29)
  
## tail -f filename

  You can continuously catch up tail of filename. 

## [dmesg](http://www.tecmint.com/dmesg-commands/)

  for log: 
  
  > dmesg 
  
  but if you use this command like "tail -f filename"
  
  > dmesg -wH

  This command operate like the above command,"tail -f filename"
  
## [tail -f filename](http://www.computerhope.com/unix/utail.htm)

 this command outputs the last part of file. 
  
## var/log/syslog (for ubuntu)

  for log

## /var/log/message or /var/log/secure (for Centos, Red Hat Family distributions)

 for log

## find
  
  I refer to [How-To Geek](http://www.howtogeek.com/112674/how-to-find-files-and-folders-in-linux-using-the-command-line/)
  
  The "find" command allows you to search for files for which you know the approximate filename.
  
   > find .
   
   The above command searched for files in current directory/
   
   the dot(.) means current directory. 
   
   To find files that match a specific pattern, Use the "-name" argument.
   
   For example, if we want to find all the files that start with "pro" in the Document Directory, we would use the "cd Document/" (without the quotes) command to chage to the Documents directory. 
   
   > find . -name pro\*
   
   for example, 
   
   find ./ -name 'vnc*'

 if you want practical example about find command, I recommend you [The Geekstuff's find](http://www.thegeekstuff.com/2009/03/15-practical-linux-find-command-examples/). 
 
 The site has many examples of usage to find commad of linux. 

## whereis

  I will recommand this command. 
  
  The whereis command shows you the location for the binary, source and mana pages for a command, 

  for simple examples, in here, refer to this [CompterHope's Whereis](http://www.computerhope.com/unix/uwhereis.htm)
  
  **Charateristics of Whereis**
  
  1. The supplied names are first stripped of leading pathname components and any (single) trailing extension of form like ".ext", ".c" and so on 
  
  2. whereis attemps to locate the desired program in a list of standard Linux places for something like binary, source, manual page files
  
  find - Find files within a directory hierarchy. 
  which - Locate the binary executable of a command. 

## unzip

 to extract the contents of a zip file, here is [a CentOS's Unzip](https://www.centos.org/docs/2/rhl-gsg-en-7.2/s1-zip-tar.html)
 
 > unzip filename.zip

## [systemctl](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

   if you want to know more about detail. I recommend you to click the above title. 
   
   In a word, 
   
   to start system
   
   > systemctl start application.service 
   
   to verify Whether status of system is active or not 
   
   > systemctl status application.service
  
## how to get sudo privilege 
 
   just refer to [this site of Digitalocean](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file-on-ubuntu-and-centos)
   
## Free
  free make you see unused RAM. 
  
  free -g 
  
   - Just -g option is to express the size of RAM in unit of gigabyte 

  [reference site 1 ](http://www.linuxnix.com/find-ram-size-in-linuxunix/) or [reference site 2](http://www.computerhope.com/unix/free.htm)
  
## CUT 

I will explain about cut command with sample, So as to tell you about cut command I refered to [this site](http://www.livefirelabs.com/unix_tip_trick_shell_script/unix_operating_system_fundamentals/introduction-to-the-unix-cut-command.htm)

`The cut command is used to extract a vertical selection of columns(charater position) or fields from ont or more files. The syntax for extracting a selection based on a column numver is :`

 > $cut -c n [filename(s)]  
 
  For example 
  
   where n equals the number of the column to extract. Consider the contents of a file namge class, as follows :
   
   > $ cat class   
   > A Johnson Sara  
   > D Smith Tom  
   > B Jones Mindy  
   > D anderson Bob  
   
   The following cut example will extract the first colum of the class file :
   
   > $ cut -c 1 class  
   > A  
   > D  
   > B  
   > D  
   
`The syntax for extracting a selection based on a field number is :`

 > $ cut -f n [filename(s)]  
  
  For example, 
  
   When n represents the number of the field to extract. the default field delimiter is the tab character. 
   
   This cut example will extract the seconde field of the class file and redirect standard output to the file class.lastname :
   
```bash
   $ cut -f 2 class > class.lastname  
   $ ls 
   $ cat class.lastname
   Johnson   
   Smith   
   Jones  
   Anderson  
```

in addition, The -d option("cut -d") can be used to change the field delimeter to something other than the default tab character as I said at the above. 

```bash
   $ cat ./delimiterFile
   emeka:x:1438:100::/home/emeka:/bin/ksh   
   shelley:x:1439:100::/home/shelley:/bin/ksh  
   dmeyer:x:1440:100::/home/dmeyer:/bin/ksh  
   kurtarn:x:1441:100::/home/kurtarn:/bin/ksh  
   abdul:x:1442:100::/home/abdul:/bin/ksh  
```
 
  when you have the above examples. You want to extract field 1, 3, you have to issue command unlike below. 
  
  > cut -f1,3 ./delimiterFile  
  
  The right way is the following : 
   
   > $ cut -d: -f 1,3 ./delimiterFile
   > emeka:1438  
   > shelley:1439  
   > dmeyer:1440  
   > kurtarn:1441  
   > abdul:1442  
  
  The colon immediately following "cut -d" instructs the cut command to look at the data in between each colon.
  
## [More](http://alvinalexander.com/unix/edu/examples/more.shtml)

  The Linux more command lets you view text file or other output in scrollable manner. It displays the text one screenfull at a time, and let you scroll backwards and forwards through the text, and even lets you search the text.

  > $ more filename
  
  instead of the following 
  
  > $ cat filename
  
  after more command, You can use these keys to move through the output :
  
    - [SPace] : scrolls the display, on screenfull of data at a time
    - [Enter] : scrolls the display one line
    - [b] : scrolls the display backwards one screenfull of data
    - [/] : lets you search the text, just like  you would inthe vi/vim editor. 
   
  [reference of another site](https://www.lifewire.com/what-to-know-more-command-4051953) 
  
  
## [less](http://www.sanfoundry.com/4-practical-less-command-examples-and-tips-effective-navigation-in-linux/)

  this command is more powerful than more command, just this command is used to veiw files instead of opening the file
  
  I prefer to use this command to veiw files than more. similarly with more, this command can move forwards and backwards. 
  
  
  less [option] filename 
  
  [referenc of another site](https://www.lifewire.com/what-to-know-less-command-4051972)

  [referenc of another site2](http://www.thegeekstuff.com/2010/02/unix-less-command-10-tips-for-effective-navigation)

## [mount](http://www.thegeekstuff.com/2013/01/mount-umount-examples/?utm_source=tuicool)

  > $ mount -t type device destination_dir
  
  This tells the kernel to attach the filesystem found on device (which is of type type) at directory of destination_dir.
  
  [Another reference](http://www.computerhope.com/unix/umount.htm) 

  the above command is different from mkfs.
  
  
## [How to list or show all mounted devices.](http://www.cyberciti.biz/faq/linux-command-list-mounted-devices-in-terminal/)

  How can you list or show all mounted devices in a terminal under Linux operating system. 
  
  you need to use one of the following. 
  
  1. [df](http://www.cyberciti.biz/faq/linux-how-to-determine-find-out-file-system-type/) - shows you file system diks space usage ([reference of tecmint](http://www.tecmint.com/how-to-check-disk-space-in-linux/)- this referenc is useful

```bash
  $ df -T
Filesystem                      Type     1K-blocks     Used Available Use% Mounted on
devtmpfs                        devtmpfs   8149892        0   8149892   0% /dev
tmpfs                           tmpfs      8160000     1960   8158040   1% /dev/shm
tmpfs                           tmpfs      8160000    17040   8142960   1% /run
tmpfs                           tmpfs      8160000        0   8160000   0% /sys/fs/cgroup
tmpfs                           tmpfs      8160000     2172   8157828   1% /tmp
/dev/sda1                       xfs         508588   136852    371736  27% /boot
tmpfs                           tmpfs      1632000       16   1631984   1% /run/user/1000
ext4                            tmpfs      2097152        0   2097152   0% /home/hyunyoung.lee/ramdisk
```

  2. mount - shows you all mounted systems. 
  
```bash
  $ mount OR $ mount -l
  proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=8149892k,nr_inodes=2037473,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
.......
```

  3. /proc/mounts or /proc/self/mounts file  - shows all mounted file systems.

## [grep](http://www.cyberciti.biz/faq/howto-use-grep-command-in-linux-unix/)

  if you click the above title, just you can see the basic concept. 
  
  Just if you want usage, I recommend [this site,Geekstuff](http://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples), That's becuase the site explain example to use grep command

  if you want to use extemded words. just ustilzie -e option. i.e, if you have mutiple words to search, 
  
  utilize -e option, as follows. 
  
  > grep -e "word1" -e "word2" FileName
  
  for above command, you can shrink one line about the above command. 
  
  like this,
  
  > grep -E 'word1\|word2' FileName
  
  explanation of above command is in [this site](http://www.thegeekstuff.com/2011/10/grep-or-and-not-operators).
  
  That's it. 
  
## dd 

  dd command means that copying a file, converting format of the data in the process, according to the operands specified.
  
  Bascially, If you want to know this command, I recommen you two sites. onte is [GNU coreutils](https://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html), The other is [compueter Hope](http://www.computerhope.com/unix/dd.htm)

  typically, people use this commnad like this. 
  
  > dd if='file' of='file' bs='2G' count=1
  
  In the above command, 
  
  > if='file' : Read from file instead of standard input, So if you don't use this command. you can enter like 'scanf' function of C language 
  
  > of='file' : Write to file instead of standard output.
  
  > bs=**bytes** : Set both input and output block size to **bytes**. This command makes dd read and write **bytes** per block, 
  
  overriding any 'ibs' and 'obs' settings. In addition, If no data-transforming conv option is specified, input is copied to the optput as soon as it's read, even if it is smaller than the block size. 
  
  > count=n : copy n 'ibs'-byte blocks from the input file, instead of everything until the end of the file 
  
  In special case, you use 'oflag=flag' option 
  
  In mycase, I use 'oflag=direct'
  
  > dd oflag=direct io=dev/zero of=dev/nvme0n1 bs=2G count=2
  
  > 'oflag=direct' : use direct I/O for data, avoiding the buffer cache, i.e this option skips the Os buffering of the writes.
  
  if you want to read details. here is [the site](http://appsintheopen.com/posts/27-test-hard-disk-speed-with-dd) 
  
## screen

  this command is useful to use. all of a sudden, when shell is stopped, this command is good.  

## cd -

  when you want to come back before one, you can use this command.
  
  but oh my zsh is use this another way, 
  
  like this, cd -l and then press 'tab' key
 
## ls /dev

## nvme list

  nvme list \| more

  nvme list \| wc -l 
  
## lspci -d 1c5c:

  lspci -d 1c5c: \| wc -l

## ping 

  ping [ip address or domain name]
  
  ping ip-address
  
  ping domain name 

## id 

  you can check current user name like this

```
$ id
uid=1(hyunyoung.lee) gid=1(hyunyoung.lee) groups=1(hyunyoung.lee) context=unconfined_u:unconfined_r:unconfined_t:s!-s!:c!.c!
```

## chown

  this command change the authority of file. 

  if you use some file with hyunyoung account. 

  sudo chown –R hyunyoung.hyunyoung /media/nvme0n1

  **this means you tell to system that you change authority of the file  to user of hyunyoung and group of hyunyoung.**
  
  if you want to check whether authority changed to what I mean.
  
  just use this command **ls -alt**
 
# Reference

 - [Computerhope's vim](http://www.computerhope.com/unix/vim.htm)
 
 - [Microshell's Split Screen in vi](http://www.microshell.com/programming/quick-tips/split-screen-in-vi/)
 
 - [Vim wikia's Resize Splits more Quickly](http://vim.wikia.com/wiki/Resize_splits_more_quickly)
 
 - [Youtube's cut, paste, copy](https://www.youtube.com/watch?v=ar8Jls9rh64)
 
 - [Vim wikea's Using Tab Pages](http://vim.wikia.com/wiki/Using_tab_pages)
 
 - [Elearning's htop](http://elearning.wsldp.com/pcmagazine/centos-install-htop/)
 
 - [The Geeksstuff's od](http://www.thegeekstuff.com/2012/08/od-command/)
 
 - [Computerhope uchmod](http://www.computerhope.com/unix/uchmod.htm)
 
 - [The Geekstuff's history](http://www.thegeekstuff.com/2008/08/15-examples-to-master-linux-command-line-history/)
 
 - [CompterHope's Scp](http://www.computerhope.com/unix/scp.htm)
 
 - [StackExchange](http://unix.stackexchange.com/questions/47909/transfer-files-using-scp-permission-denied)
 
 - [The Geekstuff's lspci](http://www.thegeekstuff.com/2014/04/lspci-examples)
 
 - [Redhat Site's lsblk](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-sysinfo-filesystems.html)
 
 - [Fibrevillage's lsblk](http://fibrevillage.com/storage/53-lsblk-command-examples)
 
 - [How-To Geek](http://www.howtogeek.com/112674/how-to-find-files-and-folders-in-linux-using-the-command-line/)
 
 - [The Geekstuff's find](http://www.thegeekstuff.com/2009/03/15-practical-linux-find-command-examples/) 
 
 - [CompterHope's Whereis](http://www.computerhope.com/unix/uwhereis.htm)
 
 - [CentOS's Unzip](https://www.centos.org/docs/2/rhl-gsg-en-7.2/s1-zip-tar.html)
 
 - [cybercit's user id](https://www.cyberciti.biz/faq/appleosx-bsd-shell-script-get-current-user/) 
