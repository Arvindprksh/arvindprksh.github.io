---
layout: post
title: Open-Channel Solid State Drive
subtitle: concise Infomation of Open-Channel SSD
category: SSD (Solid State Drives)
tags: [lightNVM]
permalink: /2016/03/07/Open-Channel_Solid_State_Drives/
---

<a href = "http://lightnvm.io"> 이 사이트 참조 </a>

Open-channel SSD 독자적인 PCI 보드를 사용을 한다.  opcode 0xe2라는 것으로 vendor에 의존적인 것이다.

lightnvm이라는 커널 모듈을 이용해서 위의 open-channel SSD를 지원을 하는데 이는 특정 규격에 맞게 설계된 보드만 lightnvm을 이용하여 일단 성능을 테스트 할 수 있다. 일단 다른 방식으로 접근을 해보자. 

Open-channel SSD는 host(kernel)가 펌웨어로 관리하던 SSD를 직접 관리하고 유지하기위한 장치이다. 펌웨어적으로 해온 것은 1. Flash Translation Layer(FTL) 2. bad block management 3. hardware units such as flash controller, the interface controller, and larger amounts of flash chips.

Open-channels SSD는 물리적 flash memory에 직접 접근을 할수 있습니다. 
즉, lihgtNVm is a specification that gives support to Open-channel SSDs. LightNVM allows the host to manage data placement, garbage collection, and parallelism. Device specific responsibilities such as bad block management, FTL extensions to support atomic IOs, or metadata persistence are still handled by the device.

The architecture of LightNVM consists of three parts : core, media manager and targets. The core implements shared fuctionality across targets. For Example initialization, teardown and statistics. The block manager implements management of flash blocks in host, and at last the targets implement the interface that exposes physical flash to user-space application. Examples of such targets include key-value store, object-store, as well as traditional block.

좀 더 자세한 정보는 <a href = "http://openchannelssd.readthedocs.org/en/latest"> Open-Channel Solid State Drives </a>

<a href = "http://openchannelssd.readthedocs.org/en/latest/gettingstarted"> reference </a>
## How to use
 Oepn-Channel SSDs require support in th kernel.LightNVM, the kernel sugsystem enablish such support is part of the vanilla Linux Kernel from 4.4+. The latest source cod is available at the Open-Channel SSD project in Github (see below)
 
 after booting the kernel. to enable LightNVM, the following must be met:
 
 1. A compatible device driver that is registered with LightNVM. For example null_blk, QEMU NVMe or an Open-Chnnel SSD, such as the CNEX Labs Westlake SDk.
 
 2. An initialized media manager on top of the device driver. Note that LightNVM provides a gerneric media manager. The Media manager maintains a list of free/in-use/bad blocks on media and exposes a get/put block API that upper layers can use to allocate into the SSD address space.
 
 3. An initialized Target on top of the block manager that exposes the SSD address space. The target can expose a traditional block I/O interface, or more esoteric interfaces such as key-values, object-stores, etc.

lnvm tool를 이용해서 한번 테스트를 해봐야 겠다.
