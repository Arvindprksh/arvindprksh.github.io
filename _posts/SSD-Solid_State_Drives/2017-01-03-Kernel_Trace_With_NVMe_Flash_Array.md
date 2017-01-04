---
layout: post
title: Process priority, CPU isolation, CPU affinity, Hyper-threading of CPU core and so on
subtitle: consideration of all flash array with NVMe for performance and user applications
category: SSD (Solid State Drives)
tags: [nvme, summary]
permalink: /2017/01/03/Kernel_Trace_With_NVMe_Flash_Array/
---

SSD itself is fast IOPs. 

But depending on application, server architecte, and administrator tools that data center use, manager and developer doesn't make a consideration of performance that consists of all flash array with NVMe.

let's see what kind of feature can affect IOPs and speed of SSD in kernel.

## Scheduler of Kernel

 objective of kernel's Scheduler is fair. So each process has priority. 
 
 Let's see How to configure what type of features in linux.
 
 If you test with fio to adapt process's priority. 
 
 **consider LINUX's chrt command**
 
## First, CPU affinity

 Processor affinity or CPU pinnig enable the binding and unbinding of a processor or a thread to a central processing unit(CPU) or a range of CPUs, 
 
 So that the process or thread will execute only on the designated CPU or CPUs rather than any cpu. This can be viewed as a modification of the native central queue scheduling algorithm in a symmetric multiprocessing operating system. 
 
 Each item in the queue has a tag indicating its kin processor. 
 
 At the time of resource allocation, each task is allocated to its kin processor in preference to others.
 
 Processor affinity takes advantage of the fact that remnants of a process that was run on a given processor may remain in that processor's state (for example, data in the cache memory) after another porcess was run on that processor. 
 
 Scheduling that process to execute on the same processor improves its performance by reducing performance-degrading events such as cache misses. 
 
 **if you use this feature with fio tools**
 
 In other words, when you use fio tool, if you want to allocate each of specific CPU core on FIO workoad threads, 
 
 at this time, you have to be careful of **cpus_allowed** option of fio.
 
## Second, Cpu isolation. 

  **This meaning is the isolcpus boot parameter can be used to specify CPUs to be isolated from the general SMP balancing and schedular algorithms.**
  
  Isolating a CPU prevents tasks/processes from being assigned to or from The CPU by the scheduler and therefore assigning processes/tasks to ro from the CPU must be done manually via the taskset, cset commands, or other software utilizing the CPU affinity syscalls.
 
## hyper-threading on the only phisical core

 Hyper-Threading is a technology used by some intel microprocessors that allows as single microprocessor to act like two separate processors to the operating system and the application programs that use it. 
 
 With Hyper-Threading, a microprocessor's "core" processor can execute two concurrent streams of instructions sent by the operating system. Having two streams of execution units to work on allows more work to be done by the processor during each clock cycle.
 
 To the operating system, the hyper-Threading microprocessor appears to be two separate processors. 

## Reference 

 - [wikipedia's Processor affinity](https://en.wikipedia.org/wiki/Processor_affinity)

 - [Symmetric mulitiprocessor system](https://en.wikipedia.org/wiki/Symmetric_multiprocessor_system)
 
 - [core vs cpu of stack overflow](http://stackoverflow.com/questions/19225859/difference-between-core-and-processor)
 
 - [cpu isolation](https://www.novell.com/support/kb/doc.php?id=7009596)
 
 - [cpu isolation's answer of stackoverfolw](http://unix.stackexchange.com/questions/208538/telling-linux-kernel-not-to-use-certain-cpus)
 
 - [intel's hyper-threading](http://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html)
 
 - [hyper-threading of Whatls.com] (http://whatis.techtarget.com/definition/Hyper-Threading)
 
 - [makeuseof's What is Hyper-Threading ?](http://www.makeuseof.com/tag/hyperthreading-technology-explained/)
   
    in this atricle, if you find out the line including "convey-belt", you have to read the paragraph in detail to understand what the hyper-threading is.
    
    if you read the paragrah, You will get a hint about hyper-Threading.
    
  - [quora's cycle graph of cpu](https://www.quora.com/What-is-clock-cycle-machine-cycle-instruction-cycle-in-a-microprocessor)
  
  - [LINUX KERNEL TRACING's opensource](http://lttng.org/)
