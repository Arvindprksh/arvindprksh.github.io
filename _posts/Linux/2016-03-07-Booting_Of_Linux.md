---
layout: post
title: Booting Of Linux
subtitle: How to boot linux - You need to upload the image. 
category: Linux
tags: [linux, concept]
permalink: /2016/03/07/Booting_Of_Linux/
---

기본적으로 컴퓨터가 부팅을 하면 
1. Bios가 기본 입출력 장치(ssd, 키보드, PCI device)랑 통신해서 각 장치 사이즈를 인식하고 
   각 장치의 base address를 설정(memory mapping-> 시작주소 + 사이즈 )을 한다. 전원이 켜지면 컴퓨터나 메모리 (ssd)은 전원이 들어온 상태이다.  
2. 그리고 bootloader가 각가 boot record를 실행을 시킨다. 그 기록에 순서대로 그리고 kernel를 실행시키고 
  kernel은 최초롤 실행을 시켜야할 프로세스(init process, 데몬프로세스 서비스프로그램)를 차근 차근 실행을 하면서 기본적인 컴퓨터 초기 세팅을 마무라한다. 
3. 그럼면 컴퓨터는 부팅이 끝이 나고 프로그램은 실행이 된다. 

자세한 과정은 <a href = "https://www.youtube.com/watch?v=DOkPZojTOhI"> 부팅 과정 영상 </a>

SSD 안에도 자그만한 컴퓨터 시스템이 있다. controller(arm core + sram) + dram + nand flash memory + capicity으로 구성이 되어있어서
하나의 컴퓨터가 하드디스크+ dram+ cpu로 연산을 하듯이 연산을 한다. 
즉 전원이 들어 왔을 때 sram에 bootload를 해야할 주소가 올라오고 각 bootload 해야할 장소에서 프로그램(firmware-rom에 있는)을 가지고온다. 
Dram logical 주소를 Phisical 주소로 매핑을 해야할 정보를 가지고 있어서 실제 nand flash memory 데이터를 읽어 온다.

nand flash memory는 overwrite는 안되지만 지웠다 쓸수는 있다. 즉 데이터를 저장하는 장치 

또 capacity는 일단은 비상용 전력장치로 전력이 차단 되었을 시 ssd를 가동 시킬수 있는 비상용 전력장치이다. 
이 장치는 보통 enterprise버전에 있다. 

또 dram, sram의 일부는 버퍼 역활을 하여 현재 nand flash memory의 모두에 다 쓰여지고 있을 시 임시로 데이터를 sram, dram버퍼 부분에
저장을 한다. 그리고 nand flash memory의 연산이 끝나면 이제 퍼버에 있는 데이터를 저장한다. 

이 처럼 ssd에도 하나의 서브 시스템이 있듯이 컴퓨터도 전체의 시스템에는 그래픽, 네트워크 등이 하나의 시스템으로 존재한다. 

![](/img/Image/Linux/2016-03-07-Booting_Of_Linux/booting_open_channel.png)

just to summarize above,

1. bios implements memory mapping that consists of base address + size 
2. kernel plays role that controlls device using device driver.

즉 커널은 중앙에서 관리하는 역할을 하고 그리고 초기 프로세서를 실행을 시켜

사용자가 컴퓨터를 사용 할 수 있는 초기 세팅을 해놓는다. 

if you need to know more, try to link <a href = "http://www.utilizewindows.com/cmos-bios-and-boot-process/">this site</a>
