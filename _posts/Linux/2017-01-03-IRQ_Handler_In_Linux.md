---
layout: post
title: What is the IRQ Handler ?
subtitle: What does the Interrupt Request and Interrupt handler mean ?
category: Linux
tags: [summary]
permalink: /2016/01/03/IRQ_Handler_In_Linux/
---

I have known concept of IRQ and handler, But I want to summarize these fundamental Before testing all flash array performance with NVMe.

## Interrupt request (PC architecture)

In a computer, an interrupt request (or IRQ) is a hardware signal sent to the processor that temporarily stops a running program and allows a special program, an interrupt handler, to run instead. hardware interrupts are used to handle events such receciving data from a modem or network card, key presses, or mouse movements.

* Interrupt of computer science have two types. one is sofrware inturrput and the other one is hardware interrupt. 

**Currently,** I will test perfomance with NVMe. I will focus my task on hardware interrupt. In detail, I will organize this concepts. 

## Interrupt Handlers

 There are two types of intercation between the CPU and the rest of the computer's hardware
 
 The first type is when the CPU gives orders to the hardware, the other is when the hardware needs to tell the CPU something.
 
 The second, called interrupts, is much harder to implement becuase it has to be dealt with when convenient for hardware, not the CPU. 
 
 Hardware devices typically have a small amount of RAM, and if you don't read their information when availble. it is lost.
 
 When the CPU receives an interrupt, it stops whatever it's doing, saves certain parameters on the stack and calls the interrupt handler. This means that certain things are not allowed in the interrupt handler itself, becuase the system is in an unknown state. The solution to this problem is for the interrupt handler to do what needs to be done immediately, usually read something from the hardware or send something to the hardware, and then schedule the handling of the new information at a later time and return. The kernel is then guarnteed to call the bottom half as soon as possible -- and when it does, evertything allowed in kernel modules will be allowed. 
 
 if you want about Interrupt handler in detail. 
 
## Reference 

 - [Wikipedia's Interrupt request](https://en.wikipedia.org/wiki/Interrupt_request_%28PC_architecture%29)
 
 - [IRQ(interrupt requse) of whatls.com](http://whatis.techtarget.com/definition/IRQ-interrupt-request)
 
 - [Interrupt Handler of tldp.org](http://www.tldp.org/LDP/lkmpg/2.4/html/x1210.html)
