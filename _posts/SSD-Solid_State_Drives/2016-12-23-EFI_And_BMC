---
layout: post
title: the EFI, EFI Shell and BMC(boardbased management controller) 
subtitle: What is the EFI, EFI Shell and BMC ? 
category: SSD (Solid State Drives)
tags: [server]
permalink: /2016/12/23/EFI_shell/
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---

When I touched server like datacenter. I experienced a various thing that I didn't know whan I was in univercity. 

So, before I forget the keyword and concept. I am going to summarize those things !

## EFI
  
  The EFI Sytem partion(ESP) is a partition on a data storage device (usually a hard disk drive or solid-state drive) that is used by computer adhering to the unified Extensible Firmware Interface (UEFI).
  
  when a computer is booted. UEFI firmware loads files stored on the EXP to start installed operating systems and various utilities.
  
  An ESP needs to be formatted with a files system.

## EFI shell

  Extensible firmware interface (EFI) brings new flexibility and opportunities to users by allowing them to work in the layer between their OS and BIOS, without altering either one.
  
  
  **I think some device has nor memory, So user can do programming on this nor memory to do something in firmware level.**
  
  at that time, user have to use the EFI shell. 
  
  This is what I understad when I dealt with server of SSD. 
  
  So, When I used server of SSD with the CentOS, sometimes I would boot into EFI shell mode or normal booting mode.
  
  **at that time. in order to fit this problem. I entered "booting menu", and then, I chaged booting device to where I want to boot.**
  
  In my case, when I configure priority of booting, firts is hard disk that I installed CentOS 7
  
## IPMI (Intelligent Platform Management Interface)  
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-12-23-EFI_And_BMC/IPMI.png)
  
  The Intelligent Platform Management Interface (IPMI) is a set of computer interface specifications for an autonomous copmture subsystem that provides management and monitoring capabilities independently of the host system's CPU, firmware(BIOS or UEFI) and operationg system.
  
  as a message-based, hardware-level interface specification, IPMI operates independently of the operating system(OS) to allow administrators to manage a system remotely in the absence of an operating system or of the system management software. 
  
  Thus IPMI functions can work in any of three scenarios. 
  
  - before an OS has booted(allowing, for example, the remote monitoring or changing of BIOS settings)
  
  - when the system is powered down
  
  - After OS or system failure - the key characteristic of IPMI compared with in-band system management such as by remote login to the operating system using SSH.
  
  **IPMI use a dedicated management LAN connection**, So if you can not access server, probably you can access server with IPMI. 
  
  That is because IPMI has another LAN connection. 
  
## BMC (boardbased management controller)

  The baseboard management controller (BMC) provides the intelligence in the IPMI architecture. And this is embedded on motherboard of a computer.
  
  Differenct types of sensors built into the computer system report to the BMC on parameteres such as temperature, colling fan speed, **power status**, operating system(OS) status, etc.
  
  The BMC monitors the sensors and can send alerts to a system administrator via the network, if any of the parameters do not stay within pre-set limits, indicating a potential failur of the system. 
  
  The administrator cas also remotely communicate with the BMC to take some corrective actions - such as resetting or power cycling the system to get a hunf OS running again. 

---

**IPMI Consists of BMC and so on, So you can controll server remotely. And For IPMI  has the dedicated LAN connection.**

each of LANs has different IP address, So, when you can not access server, I think you'd better use IPMI probaly, You can access server remotely using IPMI.

At that time you can access server remotely using IPMI, You can power server on, and then you can use server remotely again.

let's see example to check status of power.

## command that I used to check up status of machine. 

 On windows 7, after installing the ipmiutil, if you don't configur path.
 
 once, move to sourceforge directory

```
cd \Program Files
cd sourcforge
dir 
ipmiutil.exe
-- ipmiutil ver 3.00
.....
```
 First, If you don't have path of ipmiutil. 
 
 in sourcforge directory, 
 
 enter "ipmiutil.exe", after that, you can see types of command 
 
 one of the commands, we see health command to check up power status of server. 
 
```
ipmiutil.exe health -U USER-ID -P PASSWORD-of-the-user -N IP-ADDRESS-of-server

-- the above command result. 

ipmiutil ver 3.00
ihealth ver 3.00
connecting to node Server-IP-ADDRESS
BMC manufacturer = ~~~(). product = ~~~()
BMC version      = 3.39 IPMI v2.0
IPMI driver type = ~ (lan)
Power State      = ~~ (S0: working) -- this means power-on
Selftest status  = ~~~ (~~)
Chssis Status    = ~~~~ (on, see below)
.......
ipmiutil ihealth. completed successfully
```
 
  but In my case, I mainly see Power Status. 
  
And You can also power server down using health command 

```
power down command 
ipmiutil.exe reset -d -U USER-ID -P PASSWORD-of-the-user -N IP-ADDRESS-of-server

power up command 
ipmiutil.exe reset -u -U USER-ID -P PASSWORD-of-the-user -N IP-ADDRESS-of-server
```
 


## Be careful 

  using domain name, you cannot access server. in emergency method, You chang the host file 
  
  on Windows, where is hosts file ?
  
   - C:\Windows\System32\drivers\etc\hosts 
   
  And if you want to chang the hosts file. You have to get cmd in administrator
  
  you put you permitting domain name in the hosts files.
  
```
  cd $Windows
  
  dir 
```  

## Reference

 - [EFI system partition](https://en.wikipedia.org/wiki/EFI_system_partition)
 
 - [Master boot record](https://en.wikipedia.org/wiki/Master_boot_record)
 
 - [GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table)
 
 - [Stackexchange](http://superuser.com/questions/520068/efi-partition-vs-boot-partition)
 
 - [ipmiutil's site](http://ipmiutil.sourceforge.net/)

 - [IPMI](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)
 
 - Definition of out-of-band : In computer networks, out-of-band management involves the use of a dedicated channel for managing network devices. 
