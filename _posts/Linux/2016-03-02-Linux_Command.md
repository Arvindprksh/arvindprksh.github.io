---
layout: post
title: Linux Command
subtitle: So far, Linux command that I learned.
category: Linux
tags: [command, summary]
permalink: /2016/03/02/Linux_Command/
---

<strong> what is the "lsblk" </strong>
  - list block device information,In order to summarize that, lsblk Command is used to list information about all available block devices, however, it does not list information about RAM disks. Examples of block devices are hard disk, flash drives, CD-ROM
  자세한 설명은 <a href = "http://www.lintut.com/lsblk-command-list-block-device-information/">이사이트</a>

  즉 블럭장치디바이스 사용이 가능한 것을 보여주는 데, 여기서 주의할점 lihgtnvm을 설치 할시 안 보일것이다. 디바이스 인식을 했지만 아직 블럭디바이스로 쓰겠다는 등록을 안했기 때문이다. 

<strong> what is the "modprobe" </strong>
  - 모듈 적재 depmod에 의 갱신된 modules.dep에서 찾아 적재한다. insmod와 달리 해당 커널 디렉토리로 갈 필요 없이 아무 위치에서나 모듈을 적재 할 수 있다. 또한 의존성이 필요한 모듈이나 먼저 실행되어야 할 모듈이 있다면 그 모듈적재하고 해당 모듈을 적재한다. 

<strong> what is the "insmod" </strong>
 - 리눅스의 shell 명령어인 insmod이 명령어를 통해 모듈을 적재 할 수 있다. 

<strong> what is the "cat" </strong>
  - 예를 들어 cat /proc/kmsg 이면 /proc/kmsg 파일을 터미널에 출력하라는 의미이다. 

<strong> a .o file & a .ko file </strong>
  - 여기서 object file은 그냥 정확히 컴파일만 된 파일을 말한다. 우리가 아는 소스코드를 기계어로 컴파일한 파일이다. 
  - the .ko file is the object file liked with kernel automatically generated data structures and are needed by kernel.
    the .o file is the object file of moduels - the result of compiling your c files. the kernel build systems then automatically creates another C file with some data structures describing the kernel module(named module_kmod.c), compile this C file into another object file and links your object file and the object file it built together to create the .ko file 
  - the dynamic linker in the kernel that is in charge of loading kernel modules, expects to find the data structure the kernel put in the kmod object in the .ko file and will not be able to load your kernel module without them.
  - 즉 다시 용약하자면 .o file이 모듈 파일이자 컴파인된 오브젝트 파일이였지만 2.6이후로는 .o file은 그냥 컴파일된 파일이고 .ko file이 커널의 모듈파일이다. 즉 이파일로 동적링크를 통해 모듈을 실행시킨다.

좀더 자세히 알고 싶으면 <a href = "http://www.stackoverflow.com/questions/7718299/whats-an-object-file-in-c"> 여기</a>
여기 --> 추가적으로 relocatble object file, shared object file, excutable object file내용도 보면 좀 컴파일러과 링커의 역할을 이해할 수 있을 거다. 

<strong> <a href = "https://en.wikipedia.org/wiki/NVM_Express" >nvme</a></strong>
  - NVM Express, NVMe, or Non-Volatile Memory Host Controller Interface Specification (NVMHCI)는 논리적인 디바이스 인터페이스 설명서입니다. 즉, PCI를 이용하는  비휘발성(NVM(non-volatile memory) : 비휘발성 메모리의 약어 흔히 SSD(solid state drive)의 형태의 flash memory) storage에 접근을 휘한 인터페이스이다. SATA와 같은 버스를 사용하는 저장 장치도 NVMe를 지원한다.  

<strong> /proc </strong>
  - /proc 디렉토리는 가상 파일 시스템으로 커널이 메모리(RAM)에 올라간 후 각종 생산되는 정보를 기록하는 곳이므로 실질적인 물리적인 용량이 없다. 즉, 하드디스크에 저장되어 있지 않다. 
  - /proc 파일 시스템은 리눅스의 커널과 사용자 영역 사이에 일어나는 통신 채널로 사용할 수 있는 가상 파일 시스템이다. 
  - 또한, 현재 시스템의 하드웨어(CPU, RAM, 파일시스템, 인터럽트, 파티션) 정보와 현재 실행되고 있는 프로세스의 정보를 확인할 수 있고, 커널이 실행되면서 생성되는 각종 정보는 /proc에 파일로 관리되고 잇다. 
  - /proc 디렉토리에 있는 숫자는 현재 실행 되고 있는 프로세스의 ID이다. 
  - /proc은 어플리케이션과 유저가 커널 시점을 볼수 있게 해준다. 즉 커널의 현재 상태를 기록을 한다. 

<strong> /proc/kmsg </strong>
 - 커널의 의해서 출력되는 각종 상태 메시지 

<strong> <a href = "http://www.thegeekstuff.com/2012/07/elf-object-file-format/">Linux ELF object</a> </strong>
  - ELF stands for executable and linked file format. EFL is used as standard file format for object files on Linux. prior to this, the a.out file format was being used as standard but lately ELF took over the charge as a standard.
  ELF supports 1. Different Processors 2. Different data encoding 3. Different classes of machines

<strong> Debugging by printing in linux </strong> 
  - 커널을 코드를 디버깅하고 올바른지 확인을 위해서는 printk라는 함수를 이용한다.
  - 그리고 printk(---,"")에서 --- 이 부분은 다양한 loglevel를 설정할 수 있다. 그건 매크로를 활용하세 loglevel을 표시한다. 
  - loglevel를 알고 싶다면 <a href = "http://makelinux.net/ldd3/chp-4-sect-2">여기 사이트 참조</a>
  - 주로 cat /proc/kmsg를 통해 커널 현재 상태가 어떤지 확인을 해보는 쪽으로 난 디버깅 방법을 정했다. 이것 말고도 다른 방식으로 디버깅을 하는 것이 존재하고, 그에 관심이 있다면 위의 글을 한번 읽어보기 바란또 또 구글에 검색 klog, dmesg 등
  -  아래 내용은 좀더 쉽게 내용을 정리한거 <a href = "http://kothamasusatish.blogspot.com/2013/03/dmesg-printk-and-kernel-log-buffer.html"> 디버깅 쉽게 설명된 사이트 </a>
  - 즉, 요약을 하자면 kernel은 로그 메시지를 printk()을 이용하여 ring buffer에 저장할 수 있다. 
  - 이 printk("log level" "message", <argument>);란 syntax로 구성하여 작성한다.
  - cat /proc/kmsg : 커널에서 메시지가 발생할때 즉시 출력 - 이것은 overwrite가 된다. 
  - dmesg는 로그가 기록된 버퍼를 읽어오는 것이다. <a href = "http://blog.naver.com/ohjoungeun/50170891946"> 네이버 참조</a>

<strong>LVM(<a href ="net123.tistory.com/194">Logical Volume Manager</a>) </strong>
   - 가상 디스크/ 가상 파티션 즉, LVM은 다수의 디스크를 논리적으로 구서아여 하나의 디스크로 동작하는 기능이다.

<strong>grep</strong>
  - grep은 유용한 command instruction이다. 
    - grep [검색문자열] [파일이름]
    - grep [option][검색문자열] [파일이름]

이를 통해 해당 파일에서 내가 찾고자 하는 문자열이 포한 된것만 가지고 활용을 할 수 있다. 

그리고 커널을 디버깅 할때 

cat /proc/kmsg \| grep [검색문자열]
dmesg \| grep[검색문자열]

을 통해 커널 로그에서 내가 찾고자 하는 정보를 쉽게 찾을 수 있다. 

위의 grep에 대하여 더욱 자세히 알고 싶으면 <a href = "http://blog.naver.com/kdi0373/220534157878"> 이 사이트 참조 </a>

<strong>null-blk : null device</strong>

  null-blk이란 것이 있는데 이것은 아무것도 없는 상태이다. 즉 이 파일에 데이터는 써지는 작용은 하지만 그 데이터가 남아 있지 않고 지워진다. 
  
<strong> .gz file</strong>
   if you need to know more, try to click <a href = "http://www.cyberciti.biz/faq/howto-compress-expand-gz-files/">this website</a>

<strong>Vim guide for beginners</strong>
  if you want to know more, just click [this site](https://www.linux.com/learn/vim-101-beginners-guide-vim)
  
  
[Semaphore VS mutex](http://www.geeksforgeeks.org/mutex-vs-semaphore/)  

   - Semaphore is sinaling mechanism
   
   - mutex is locking mechanism.

## [RPM Package](http://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/)

If you want to install rpm file with rpm command

```
 rpm -ivh ~~~~~~~.rpm
```
  
